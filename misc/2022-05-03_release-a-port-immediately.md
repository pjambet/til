# Release a port immediately

Use the `socket.SO_REUSEADDR` flag when creating a TCP server so that killing
the server immediataly releases the port. Without a quick restart can error out
with a "port already in use" error, and this can be SUPER annoying!

Example how to set the flag in python:

```python
server.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
```

And in C:

```c
int enable = 1;
if (setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &enable, sizeof(int)) < 0)
    error("setsockopt(SO_REUSEADDR) failed");
```

Links:

https://mobile.twitter.com/zeroprimezero/status/1271837883406712832
https://stackoverflow.com/questions/24194961/how-do-i-use-setsockoptso-reuseaddr
