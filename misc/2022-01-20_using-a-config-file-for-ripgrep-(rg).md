# Using a config file for ripgrep (rg)


You can use a config file with ripgrep. See [the official docs][1]. Note that
you absolutely need to set `RIPGREP_CONFIG_PATH`, in my case in `~/.zshenv`,
and that you can't use `~`, I had it as `~/.ripgreprc` at first and it didn't
work. I had to set it as:

```
export RIPGREP_CONFIG_PATH="$HOME/.ripgreprc"
```

And I used it with:

```
--context=5
```

Because I like having context

[1]:https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#configuration-file
