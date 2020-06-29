# Removing/Altering Key Bindings from Minor Mode Keymaps

I wanted to bind `C-a` to `beginning-of-visual-line` when editing markdown files, which I did with the following:

First enable `visual-line-mode` when editing markdown files:

```elisp
(add-hook 'gfm-mode-hook #'visual-line-mode)
```

And bind `C-a` to `beginning-of-visual-line` when in the visual line mode

```elisp
(add-hook 'visual-line-mode
          (lambda ()
            (define-key visual-line-mode-map (kbd "C-a") 'beginning-of-visual-line)))
```

The problem was that `C-a` [was already bound in prelude][prelude-link], to
`crux-move-beginning-of-line`:

I knew how to unbind it, with something like

```elisp
(add-hook 'gfm-mode-hook
          (lambda ()
            (define-key prelude-mode-map (kbd "C-a") nil)))
```

But it apparently always unbind it, since it's been removed from the keymap, as
I still wanted to keep the `C-a` binding, I like it when editing other files,
like Ruby for instance.

The solution was to do the following,

```elisp
(defun my-gfm-mode-hook ()
  (let ((oldmap (cdr (assoc 'prelude-mode minor-mode-map-alist)))
        (newmap (make-sparse-keymap)))
    (set-keymap-parent newmap oldmap)
    (define-key newmap (kbd "C-a") nil)
    (make-local-variable 'minor-mode-overriding-map-alist)
    (push `(prelude-mode . ,newmap) minor-mode-overriding-map-alist))
  )

(add-hook 'gfm-mode-hook 'my-gfm-mode-hook)
```

Once again, thanks to Bozhidar Batsov!

Source: https://emacsredux.com/blog/2013/09/25/removing-key-bindings-from-minor-mode-keymaps/


[prelude-link]:https://github.com/bbatsov/prelude/blob/dd9b01a991c9599842ba88e52fe6ae8627f4a782/core/prelude-mode.el#L46
