# Carriage Return resets the cursor position

**tl;dr; The Carriage Return character resets the cursor position at the
beginning on the line when writing text in a shell**

I was really confused when reading the following line on [this article][1]
about zsh:

> The indicator is shown, and since we have written exactly $COLUMN characters,
> the cursor is after the last column. Step 3, a carriage return, now moves it
> back to the start:

The piece about carriage return didn't "click" for me, until I realized that it
is indeed a "carriage return", in the typewriter sense, as in, the carriage
returns to the beginning of the line.

This example summarizes it well:

```
echo -n this-is-written-first && echo -n "\r" && echo -n pierre
# > pierres-written-first
```


[1]: https://www.vidarholen.net/contents/blog/?p=878
