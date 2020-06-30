# SVG Stroke & Fill properties

As I was setting up the social icons for pacing.pjam.me, I encoutered
a few issues with the styling of the SVG icons when adding one for
Strava.

Based on [this issue](https://github.com/MunifTanjim/minimo/issues/248) I ended
up using icons from https://simpleicons.org/ instead of the ones from
https://feathericons.com/

After replacing the SVG content, the styling looked off and I had to modify the
`stroke` and `fill` properties, respectively to `initial` and `inherit` to
prevent weird styling that I still can't really explain and is probably
inherited from other parts of the minimo theme

See:

- https://css-tricks.com/almanac/properties/s/stroke/
- https://css-tricks.com/almanac/properties/s/fill/
- https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Fills_and_Strokes
