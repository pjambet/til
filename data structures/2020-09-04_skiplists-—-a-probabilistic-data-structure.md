# Skiplists — a probabilistic data structure

Heard about this for the first time while digging in the Redis code base,
specifically in the `t_zset.c` file which implements the sorted set related
commands.

The main structure is defined in [`server.h`][1]

To quote wikipedia:

> In computer science, a skip list is a probabilistic data structure that
> allows O(logn) search complexity as well as O (logn) insertion complexity
> within an ordered sequence of n elements.

> Thus it can get the best features of a sorted array (for searching) while
> maintaining a linked list-like structure that allows insertion, which is not
> possible in an array. Fast search is made possible by maintaining a linked
> hierarchy of subsequences, with each successive subsequence skipping over fewer
> elements than the previous one (see the picture below on the right). Searching
> starts in the sparsest subsequence until two consecutive elements have been
> found, one smaller and one larger than or equal to the element searched for.
> Via the linked hierarchy, these two elements link to elements of the next
> sparsest subsequence, where searching is continued until finally we are
> searching in the full sequence. The elements that are skipped over may be
> chosen probabilistically or deterministically, with the former being more
> common.


Read more on [wikipedia][2]

What did you learn about data structures today

[1]:https://github.com/antirez/redis/blob/6.0/src/server.h#L899-L914
[2]:https://en.wikipedia.org/wiki/Skip_list

