# Move cursor when priting to terminal

What did you learn about unix today

You can move the cursor when priting to a terminal by using the following ANSI escape sequences:

- Position the Cursor:
  \033[<L>;<C>H
     Or
  \033[<L>;<C>f
  puts the cursor at line L and column C.
- Move the cursor up N lines:
  \033[<N>A
- Move the cursor down N lines:
  \033[<N>B
- Move the cursor forward N columns:
  \033[<N>C
- Move the cursor backward N columns:
  \033[<N>D

- Clear the screen, move to (0,0):
  \033[2J
- Erase to end of line:
  \033[K

- Save cursor position:
  \033[s
- Restore cursor position:
  \033[u

Example

The following output contains three spaces between my first and last name, because we moved the cursor three columns to the right:

```
echo -n "pierre" && echo -n "\033[3C" && echo -n "jambet"
# > pierre   jambet
```

Source: https://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x361.html
