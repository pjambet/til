# malloc vs calloc

From `man 3 malloc` I read the following:

> The malloc() function allocates size bytes of memory and returns a pointer to the allocated memory.

&

> The calloc() function contiguously allocates enough space for count objects that are size bytes of memory each and returns a pointer to the allocated memory. The allocated memory is filled with bytes of value zero.

But it was still a bit unclear to me what the different use cases would be given that, as the SO question linked below states, these two look very similar:

``` c
ptr = (char **) malloc (MAXELEMS * sizeof(char *));
ptr = (char **) calloc (MAXELEMS, sizeof(char*));
```

The short answer seems to be, if you don't care about the existing bytes values of the address allocated, use `malloc`, this is the case when you know you'll write there right after allocating.

But in some cases you might want to clear all the existing shit that was there before (if any?) and that's what `calloc` does, it sets all the bytes to zero, which I guess comes at a (small?) cost.

The comment from the accepted answer was illuminating:

> The *alloc variants are pretty mnemonic - clear-alloc, memory-alloc, re-alloc

So it's not so much that `malloc` is for "regular" stuff and `calloc` is for arrays, which I initially thought.

More on [StackOverflow](https://stackoverflow.com/questions/1538420/difference-between-malloc-and-calloc)
