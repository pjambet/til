# Why there's no ZDIFF[STORE] command(s) (for now)

Redis supports two types of sets, "regular", with commands prefixed with `S`,
such as `SADD` and "sorted sets" with commands prefixed with `Z`. Most of the
commands available for unsorted sets, such as SINTER[STORE] & SUNION[STORE]
have a sorted equivalent, such as ZINTERSTORE & ZUNIONSTORE. Not that 6.2, not
released yet, will add ZINTER & ZUNION.

BUT! There is a way to compute the diff of sets with ZDIFF/ZDIFFSTORE, but not
equivalent commands for sorted sets!

I found some old discussions and a proposal for such a command, here's a summary:

PR (From 2012!) to add ZDIFFSTORE: https://github.com/redis/redis/pull/448

The reason why it's not already a command can be summarized from this comment
from Pieter Noordhuis on 12/9/2010
(https://groups.google.com/g/redis-db/c/Ti93ilzdyYw/m/jCo1QrMLgncJ):

> ZDIFFSTORE makes no sense, as discussed before on the ML (please search
> before posting). The intrinsic value of the scores gets lost when you simply
> start subtracting them. So, instead, you can use e.g. ZUNIONSTORE with WEIGHTS
> 1 -1 -1 ... and do a ZRANGEBYSCORE to get everything with score >= 1.

It took me a while to really understand what he meant, because in my mind, the
diff of sorted sets _could_ make sense, but I _think_ I get it now:

With ZUNION & ZINTER, you never discard any of the scores, even though you can
alter them with the WEIGHTS option, the result takes into account all the
scores, but with a diff, you'd have to drop some scores, here is an example:

```
s1 = { < 30, 'pierre' >, < 25, 'jane' >, < 35, 'john' > } # A sorted of unique user names and their age is the score
s2 = { < 28, 'john' > }
```

Computing `ZDIFF s1 s2`, aka `s1 - s2`, _could_ be the set: `{  < 30, 'pierre'>, < 25, 'jane' >  }`, 
but that would mean that the score of `john` in the second set, `28`, was completely ignored.

Interestingly, in a different thread from earlier that year, Peter didn't seem
opposed to the idea:
https://groups.google.com/g/redis-db/c/8X9pZ2EIhlU/discussion
