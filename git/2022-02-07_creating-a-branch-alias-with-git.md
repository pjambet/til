# Creating a branch alias with git

I've recently been working on a few different repos with different default
branch names, some use `main`, some `master`. The issue is that sometimes I use
Ctrl-R to search my history, but for instance, I'm on a repo where the default
is `master` and I want to check all ther merged branches, but the first hit in
the history is `git branch --merged main`.

What I want is a way to alias `default` to `main` in some repos, and alias it
to `master` in others, so that I can use `default` in commands, and it resolves
to `main` or `master`. That way I don't have to worry about what I find the
history and I can use it

This is how you do it:

``` bash
# Alias from default to main
git symbolic-ref refs/heads/default refs/heads/main
# Alias from default to master
git symbolic-ref refs/heads/default refs/heads/master
```
