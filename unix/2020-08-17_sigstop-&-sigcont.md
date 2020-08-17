# SIGSTOP & SIGCONT

I started a process (The Redis in Ruby thingy) in an ec2 instance after ssh-ing
into it, and closed that session. I was wondering if there was a way to "get
control back" of the parent process, like be in the same setup as I was when
starting the process. I can see the process with `ps`, but I don't want to kill
it. It looks like the answer is to use screen or tmux, so no luck here.

BUT!

As I was googling, I found out about two signals I had never heard of before,
`STOP` & `CONTINUE`. I tried it locally on `macOS`: `kill -17 pid` to stop and
`kill -19 pid` to continue and that seems to work.

I was able to use it on my ec2 instance as well: `kill -STOP pid`, and `kill
-CONT` pid`.

Not really sure what the real life use cases for these would be, but that
sounded interesting!

Sources:

https://unix.stackexchange.com/questions/29692/how-can-i-manage-jobs-after-i-disconnect-from-my-tty-ssh-session
https://major.io/2009/06/15/two-great-signals-sigstop-and-sigcont/
