# Git Revision Format

Git has an extensive format to expression revisions

For years I've only used HEAD and the `~` operators, as in `HEAD~1`, `HEAD~4`,
etc ...

- `@` means `HEAD`
- `^` means parent


Useful examples:

- `@^^` => two commits before `HEAD`
- `@~3` => three commits before `HEAD`


https://git-scm.com/docs/gitrevisions


Thank you Building Git for teaching once again something new about git!
