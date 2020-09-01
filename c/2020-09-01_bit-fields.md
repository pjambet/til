# Bit fields

If you want to optimize things in C you can use the `:` notation to specify how
many bits you want to use, read more on
[geeksforgeeks](https://www.geeksforgeeks.org/bit-fields-c/)

Redis uses this a lot like for this struct:

``` c
/* quicklistNode is a 32 byte struct describing a ziplist for a quicklist.
 * We use bit fields keep the quicklistNode at 32 bytes.
 * count: 16 bits, max 65536 (max zl bytes is 65k, so max count actually < 32k).
 * encoding: 2 bits, RAW=1, LZF=2.
 * container: 2 bits, NONE=1, ZIPLIST=2.
 * recompress: 1 bit, bool, true if node is temporarry decompressed for usage.
 * attempted_compress: 1 bit, boolean, used for verifying during testing.
 * extra: 10 bits, free for future use; pads out the remainder of 32 bits */
typedef struct quicklistNode {
    struct quicklistNode *prev;
    struct quicklistNode *next;
    unsigned char *zl;
    unsigned int sz;             /* ziplist size in bytes */
    unsigned int count : 16;     /* count of items in ziplist */
    unsigned int encoding : 2;   /* RAW==1 or LZF==2 */
    unsigned int container : 2;  /* NONE==1 or ZIPLIST==2 */
    unsigned int recompress : 1; /* was this node previous compressed? */
    unsigned int attempted_compress : 1; /* node can't compress; too small */
    unsigned int extra : 10; /* more bits to steal for future usage */
} quicklistNode;
```

https://github.com/redis/redis/blob/6.0.0/src/quicklist.h#L46-L57

Note: it took me a while to figure out why it was 32 bytes, so here you go:

8 for each of the first three pointers, a pointer is always a 64-bit integer on
a 64-bit machine apparently, so that's 24 (8*3) bytes right there.
The first int, `sz` adds 4, we're at 28.
The next bit field optimized field all fit in a single `int` (4 bytes):

```
16 + 2 + 2 + 1 + 1 + 10 = 32 (8*4)
```

28 + 4 = 32, 32 bytes, done!
