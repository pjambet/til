# Set fill-column for git commit

Even though I've know for a while that it's common to customize variables per
mode with hooks, I ALWAYS forget how to do it.

I recently set my default `fill-column` to 120, because I like it as a default,
but I still want 72 when writing commit messages in magit, this is how you do it:

```lisp
(add-hook 'git-commit-mode-hook
          (lambda ()
            (set-fill-column 72)))
```

Sources:

- https://github.com/magit/magit/issues/3067
- https://stackoverflow.com/a/8080547/919641
