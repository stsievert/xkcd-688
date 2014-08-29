
## XKCD #688

![xkcd comic](self_description.png)


XKCD has an interesting plot in [#688]. They do a several plots that include
information about the plot in the comic. At first, this seems hard to
implement. While I was writing the simple code, I was thinking that I would
have to use a binary search or use some fancy method.

But no, since the image is correct and gradually converges to some value, you
just call the function over and over again.


[#688]:https://xkcd.com/688/
