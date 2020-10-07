# Adding man pages to an ubuntu box running through Vagrant

I tried running `man 2 write` on a Vagrant box running Ubuntu
"hashicorp/bionic64" only to be welcomed with:

```
No manual entry for write in section 2
See 'man 7 undocumented' for help when manual pages are not available.
```

Turns out I had to install them.

I found the following on SuperUser: 

```
sudo apt install manpages-posix
```

Source: https://superuser.com/questions/1349001/cant-show-manual-pages-for-ls-in-vagrant

But apparently I had to run

```
sudo apt install manpages-dev
```

Source https://www.linuxquestions.org/questions/linux-software-2/error-viewing-manpages-for-read-write-printf-566762/
