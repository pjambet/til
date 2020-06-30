# Navigate to the last location with `-`

Didn't actually learn that today, but I wanted it in this repo.

Use `-` with `cd` to mean "the previous location", here is an example:

```
~
❯ cd -
~/dev/til

~/dev/til master
❯ cd ../sandbox/til-rb

~/dev/sandbox/til-rb trunk ⇣
❯ cd -
~/dev/til

~/dev/til master
❯ cd -
~/dev/sandbox/til-rb
```

In the previous example, we're starting from my home directory, `~`, manually
`cd`-ing in `~/dev/til`, then manually `cd`-ing in `~/dev/sandbox/til-rb`, and
then going back to `~/dev/til` by using `cd -`, and then back to
`~/dev/sandbox/til-rb` by running `cd -` again. You can think of it as the
"Last" button on your TV remote, if you keep on pressing it, you will toggle
between the last channel and the one you're currently watching, and so on. Same
here!

The best part, it also works with `git checkout`!

```
~/dev/blog master
❯ gco -b new-branch
Switched to a new branch 'new-branch'

~/dev/blog new-branch
❯ gco master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

~/dev/blog master
❯ gco new-branch
Switched to branch 'new-branch'

~/dev/blog new-branch
❯ gco -
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

~/dev/blog master
❯ gco -
Switched to branch 'new-branch'
```

It might also work in other places, but if so, I'm not aware of it (yet)
