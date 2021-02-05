# Prevent Ctrl-D from accidentally killing a shell

Seems like these options are possible, but only the second one seems to work
with zsh, so I added it to my zshrc file!

```
IGNOREEOF=10   # Shell only exists after the 10th consecutive Ctrl-d

set -o ignoreeof  # Same as setting IGNOREEOF=10
```

Seems like another option would be `stty eof undef`

Source: https://superuser.com/questions/479600/how-can-i-prevent-tmux-exiting-with-ctrl-d/479614
