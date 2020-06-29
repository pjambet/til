# Disable ruby-rubocop when editing code blocks

This one was a real pain in the ass. I started using `edit-indirect` to edit
code blocks when writing in markdown, with `C-C '`, which I absolutely love,
the only problem was that my ruby mode is configured to load flycheck, and
includes the `ruby-rubocop` checker by default, which I usually want when I
write _real_ ruby, but for reasons I really don't understand, was throwing an
error when loaded in the indirect buffer:

https://github.com/flycheck/flycheck/issues/1504

So, because I don't really care about rubocop checks when editing a small code
block, I wanted to just turn it off in this context, it took me ages to figure
out how to do it and I ended up with the following in my
`.emacs.d/custom/personal.el` file (I use prelude)

```elisp
(add-hook 'edit-indirect-after-creation-hook
          (lambda()
            (setq flycheck-disabled-checkers '(ruby-rubocop))))
```

I found the edit indirect hook by looking at the code on GitHub:
https://github.com/Fanael/edit-indirect/blob/935ded353b9ed3da67bc61abf245c21b58d88864/edit-indirect.el#L59

Three hours I'll never get back 😭
