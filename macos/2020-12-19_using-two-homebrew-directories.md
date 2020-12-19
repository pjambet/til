# Using two homebrew directories


One for x86_64, one for arm64.

x86_64 go into `/usr/local`:

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

This might change when arm64 is supported by default, but this script has this section:

```
# On macOS, this script installs to /usr/local only.
# On Linux, it installs to /home/linuxbrew/.linuxbrew if you have sudo access
# and ~/.linuxbrew otherwise.
# To install elsewhere (which is unsupported)
# you can untar https://github.com/Homebrew/brew/tarball/master
# anywhere you like.
if [[ -z "${HOMEBREW_ON_LINUX-}" ]]; then
  HOMEBREW_PREFIX="/usr/local"
  HOMEBREW_REPOSITORY="/usr/local/Homebrew"
  HOMEBREW_CACHE="${HOME}/Library/Caches/Homebrew"
# ...
```

Running this will also update the PATH variable so that `/usr/local/bin/brew` is in there.

You'll then need to prefix every `brew install xxx` with `arch -x86_64`

If you want to install arm64 formulae in parallel, run:

`curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew` in `/opt`, and use `/opt/homebrew/bin/brew`, if you don't want to add `/opt/homebrew/bin` in your PATH for now, which would probably create some conflict with the ones in `/usr/local/`

