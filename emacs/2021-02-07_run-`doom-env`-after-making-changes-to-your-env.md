# Run `doom env` after making changes to your env

It's in the FAQ [1] so there's not much I can complain about.

Anyway, I was making changes to my env (and PATH) to have `gopls` in there so I
could use the sweet sweet LSP features with go, and after spending way too much
time trying to figure out why things seemed weird with how Emacs loads env var,
turns out my solution was to re-run `doom env` to re-generate the
`~/.emacs.d/local/env` file.

Turns out that running `open /Applications/Emacs.app` is not the same as
double-clicking on `Emacs.app` in `/Applications` or running it from Alfred,
the `open` version does give you what's currently in the path, the GUI
approach, nope.


[1]: https://github.com/hlissner/doom-emacs/blob/64922dd3011eca0c263d900c5f2100af761df8bf/docs/faq.org#when-should-and-shouldnt-i-use-bindoom
