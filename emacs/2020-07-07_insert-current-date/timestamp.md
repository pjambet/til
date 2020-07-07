# Insert current date/timestamp

I have the following functions defined in my `~/.emacs/personal/custom.el` file (I use prelude):

```elisp
(defun timestamp ()
  (interactive)
  (insert (format-time-string "%Y-%m-%dT%H:%M:%S%:z")))

(defun today ()
  (interactive)
  (insert (format-time-string "%Y-%m-%d")))
```

I use them with `M-x` and then use the helm popup to find them.

Really convenient to change the date or time in the front matter of a hugo post for instance
