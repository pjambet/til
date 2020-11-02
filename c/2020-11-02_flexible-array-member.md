# Flexible array member

If the last element of a C struct is an array, `sizeof` will consider it empty

Got there from: https://redis.io/topics/internals-sds and created this small
program that outputs 16:

```c
#include <stdio.h>

struct sdshdr {
    long len;
    long free;
    char buf[];
};

int main() {
  struct sdshdr s;
  printf("sizeof(s): %lu\n", sizeof(s));
  return 0;
}
```

See wikipedia: https://en.wikipedia.org/wiki/Flexible_array_member
