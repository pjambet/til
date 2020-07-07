# Count words for all files in a folder

I wanted to run `wc` to count all the words for the different chapters of
redis.pjam.me, they're all the same folder, so I thought about `ls`, `|` and
`xargs` but my first attempt failed and it took me a while to get it, the
answer wasn't that crazy but anyway, here it is:

```
ls content/post/* | xargs wc
```

Result:

```
     492    3707   26408 content/post/chapter-1-basic-server.md
     605    3669   23845 content/post/chapter-2-respond-to-get-and-set.md
     468    4427   30339 content/post/chapter-3-multiple-clients.md
      24      53     377 content/post/chapter-4-completing-set-and-more-string-commands.md
    1589   11856   80969 total
```
