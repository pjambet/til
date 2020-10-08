# Revision format, Ancestry references, and merge commits

I was reading [Building Git](https://shop.jcoglan.com/building-git/), Chapter
17.1, and was confused by the following:

```
$ git cat-file -p @^1^{tree}
100644 blob 0cfbf08886fca9a91cb753ec8734c84fcbe52c9f f.txt
100644 blob d00491fd7e5bb6fa28c517a0bb32b8b506539d4d g.txt

$ git cat-file -p @^2^{tree}
100644 blob d00491fd7e5bb6fa28c517a0bb32b8b506539d4d f.txt
100644 blob 00750edc07d6415dcc07ae0351e9397b0222b7ba g.txt
```

Especially, the `@^1^{tree}` & `@^2^{tree}` bits, so here we are:

First thing first, `@` is an alias for `HEAD`, as of Git 1.8.5:
https://github.com/git/git/blob/v1.8.5/Documentation/RelNotes/1.8.5.txt#L100-101

Thank you StackOverflow for this: https://stackoverflow.com/a/17910097/919641


- @^ Means the first parent of HEAD/@, it is equivalent to @~, HEAD^ & HEAD~
- The last bit ^{tree} is because by default you'd get the commit object, which
  you can request with ^{commit}, but why would you, it's the default
- Now, ^ vs ~ is interesting for merge commits, where you can have more than
  one parent, and ^2 means, the second parent, where usually the first parent is
  the one on the branch you were when you merged (usually master)

So what this all means is that you could also say "Go back two commits", with
`@~~`, `@^^`, `@~2`, but if you say `@^2`, you would either go back to the
second parent, if there's one, which only happens for a merge commit, or an
error otherwise.


Documentation:
- https://git-scm.com/book/en/v2/Git-Tools-Revision-Selection
- https://git-scm.com/docs/gitrevisions

