# malloc doesn't necessarily allocate the exact number of bytes you ask for

It turns out that `malloc` might allocate more than you ask for, and this is why some platforms (like macOS) provice a `malloc_size` method.

``` c
#include <stdio.h>
#include <stdlib.h>
#include <malloc/malloc.h>

int main() {

  unsigned char *p = malloc(8);
  size_t size = malloc_size(p);
  unsigned char *p2 = malloc(17);
  size_t size2 = malloc_size(p2);
  printf("%p\n", p);
  printf("%p\n", p2);
  printf("%zu\n", size);
  printf("%zu\n", size2);

  void *newptr = realloc(p, 16);
  printf("%p\n", newptr);
  printf("%p\n", p);

  free(p);
  if (p != newptr) {
    free(newptr);
  }
  return 1;
}
```

produces the following:

``` bash
❯ ./test
0x7fd970c05900
0x7fd970c05910
16
32
0x7fd970c05900
0x7fd970c05900
```

Which I guess is a good thing because it means that `realloc` might not have to
move all the memory to a new place, since it might already have the space you
need
