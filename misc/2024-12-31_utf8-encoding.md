# UTF8 encoding

For multi byte UTF-8 character, like the japanese hiragana こ, we can get its ordinal value in Ruby with `'こ'.ord`, which returns 12371, this is the equivalent of the hex string `0x3053`, which is correct according to the UTF8 standard.

Now, we can also get the bytes in the string, with `'こ'.bytes`, which returns `[227, 129, 147]`, but to understand how these values relate to `3053`, aka `12371`, aka `00110000 01010011` (`'こ'.ord.to_s(2)`), we need to understand the UTF8, encoding, which is beautifully explained in the linked SO post below, so, if we print our three bytes as a bit string we get:

```
*1110*0011 *10*000001 *10*010011
```

The stars wrap the data that is for the UTF8 encoding, we're left with `0011`, `000001` & `010011`, which happens to be ... drum roll, 12371!

Source:

- https://stackoverflow.com/questions/44565859/how-does-utf-8-encoding-identify-single-byte-and-double-byte-characters
- https://www.unicode.org/charts/PDF/U3040.pdf
