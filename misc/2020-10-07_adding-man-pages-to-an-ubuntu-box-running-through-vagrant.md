# Adding man pages to an ubuntu box running through Vagrant

I tried running `man 2 write` on a Vagrant box running Ubuntu
"hashicorp/bionic64" only to be welcomed with:

```
No manual entry for write in section 2
See 'man 7 undocumented' for help when manual pages are not available.
```

Turns out I had to install them, I ran `sudo apt-get update && sudo apt-get
upgrade -y` and they showed up but apparently I could have also ran: `sudo apt
install manpages-posix`

Source: https://superuser.com/questions/1349001/cant-show-manual-pages-for-ls-in-vagrant
