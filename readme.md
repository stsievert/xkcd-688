
## XKCD #688
XKCD [#688] is meta -- it includes information about itself. Why not try and
recreate it?

![xkcd comic](self_description.png)

![animation](out.gif)

Of course, there are certain inaccuracies. I didn't try and make the bars the
*exact* same width and the like. The last panel doesn't accurately portray the
comic, as the resolution isn't high enough. All that aside, this script works
in general.

It turns out that this is an example of [fixed-point iteration]. In essence,
that's just using Newton's method to estimate the original function (which just
says this pixel is black, this pixel is white). The core of this algorithm is
just a for-loop; the function always returns a correct value for the current
estimate! As you might guess, this estimate might become unstable.

According to [Prof. Jarvis Haupt], this algorithm could *possibly* become
unstable. Because the third panel has an [infinite regression], it *might* be
possible to set up a [non-contractive map] where the sequence grows too much and
never converges. I couldn't get my comic to be unstable; I'm guessing that it's
stable regardless of the sizing and round-off issues I faced.

[Prof. Jarvis Haupt]:http://www.ece.umn.edu/~jdhaupt/

This is abstract and non intuitive; you can't see it in the real world. To see
it in the real world, let's pretend we have the equation

![x = r*x*(1-x)](https://upload.wikimedia.org/math/a/3/3/a333fd3f242146b32e439812cf2b00fb.png)

To implement this equation, we would only do

```python
def f(x): return 3.2 * x * (1 - x)
a = 0.5
while True:
    a = f(a)
```

Your intuition would might tell you this algorithm is stable. The first value
of the function is less that 1; shouldn't it decay like 1/n?

Well, no. That value is passed to the function again, giving f(f(a)) = 0.512.
This problem gets incredibly complex, especially if you consider any value of r
and just 3.2. It turns out that for this particular function, there's a plot
graphing the "stable" or settling points given a value of r.

![settling points](https://commons.wikimedia.org/wiki/File:LogisticMap_BifurcationDiagram.png#mediaviewer/File:LogisticMap_BifurcationDiagram.png)

As you can see, for certain values of r, this is unstable. For other values of
r, this algorithm is stable at different points. Of course, there's a whole
field of study behind this. Stability and chaos experts study similar problems
in great depth. I don't know the details to explain the full stability,
especially the reason there are stable regions surrounded by unstable regions.

[infinite regression]:http://en.wikipedia.org/wiki/Infinite_regress
[non-contractive map]:https://en.wikipedia.org/wiki/Contraction_mapping
[fixed-point iteration]:https://en.wikipedia.org/wiki/Fixed-point_iteration
[#688]:https://xkcd.com/688/
