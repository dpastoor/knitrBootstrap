<!--
%\VignetteEngine{knitr::knitr}
%\VignetteIndexEntry{Illusions example}
%\VignetteDepends{grid, plyr}
-->

# Illusions #
The R implementations for these are from Kohske Takahashi[(@kohske)](https://twitter.com/kohske).
See http://rpubs.com/kohske/R-de-illusion
from [statmethods.net](http://www.statmethods.net/advgraphs/ggplot2.html)

## Cafe wall illusion ##
All the lines are actually parallel.

<div class="chunk" id="illusions_cafe_wall"><div class="rcode"><div class="source"><pre class="knitr r">library(grid)
rs <- expand.grid(x = seq(0, 1, 1/10), y = seq(0, 1, 1/10))
grid.rect(rs$x, rs$y, 1/10/2, 1/10/2, gp = gpar(fill = "black", col = NA))
grid.rect(rs$x + 1/10/4, rs$y + 1/10/2, 1/10/2, 1/10/2, gp = gpar(fill = "black", col = NA))
ls <- expand.grid(x = 0:1, y = seq(0, 1, 1/20) - 1/20/2)
grid.polyline(ls$x, ls$y, id = gl(nrow(ls)/2, 2), gp = gpar(col = "grey50", lwd = 1))
</pre></div>
<div class="rimage default"><img src="figure/illusions_cafe_wall.png" title="plot of chunk illusions_cafe_wall" alt="plot of chunk illusions_cafe_wall" class="plot" /></div>
</div></div>


## Ouchi ##
Move your frame of reference to see the effect.

<div class="chunk" id="illusions_ouchi"><div class="rcode"><div class="source"><pre class="knitr r">grid.newpage()
nx <- 10; ny <- 30
rs <- expand.grid(x = seq(0, 1, 1/nx/2), y = seq(0, 1, 1/ny/2))
grid.rect(rs$x, rs$y, 1/nx/2, 1/ny/2, gp = gpar(col = NA, fill = c("black", "white")))
rs <- expand.grid(x = seq(0.25, 0.75, 1/nx/2), y = seq(0.25, 0.75, 1/ny/2))
grid.rect(rs$y, rs$x, 1/ny/2, 1/nx/2, gp = gpar(col = NA, fill = c("black", "white")))
</pre></div>
<div class="rimage default"><img src="figure/illusions_ouchi.png" title="plot of chunk illusions_ouchi" alt="plot of chunk illusions_ouchi" class="plot" /></div>
</div></div>


## Fraser illusion ##
All the lines are actually parallel.

<div class="chunk" id="illusions_fraser"><div class="rcode"><div class="source"><pre class="knitr r">library(plyr)
grid.newpage()
n <- 10; ny <- 8; L <- 0.01; c <- seq(0, 1, length = n); d <- 1.2*diff(c)[1]/2
col <- c("black", "white")
x <- c(c-d, c, c+d, c)
y <- rep(c(0, -d, 0, d), each = n)
w <- c(c-d, c-d+L, c+d, c+d-L)
z <- c(0, L, 0, -L)
ys <- seq(0, 1, length = ny)
grid.rect(gp = gpar(fill = gray(0.5), col = NA))
l_ply(1:ny, function(i) {n
  if (i%%2==0) {
    co <- rev(col)
    z <- -z
  } else {
    co <- col
  }  
  grid.polygon(x, y + ys[i], id = rep(1:n, 4), gp = gpar(fill = co, col = NA))
  grid.polygon(w, rep(z, each = n) + ys[i], id = rep(1:n, 4), gp = gpar(fill = rev(co), col = NA))
})
</pre></div>
<div class="rimage default"><img src="figure/illusions_fraser.png" title="plot of chunk illusions_fraser" alt="plot of chunk illusions_fraser" class="plot" /></div>
</div></div>


## Fraser-Wilcox illusion ##

<div class="chunk" id="illusions_fraser_wilcox"><div class="rcode"><div class="source"><pre class="knitr r">grid.newpage()
No <- 3
wo <- 1/3/2
po <- seq(0, 1, by = wo)[(1:No) * 2]
Nc <- 8
tc <- seq(pi * 11/12, pi * 1/12, len = Nc)
px <- c(outer(wo * cos(tc), po, `+`))
wc <- rep(sin(tc), No)
ag <- rep(1:No, each = Nc)
dc <- 21
th <- seq(0, 2 * pi, len = dc)
grid.rect(gp = gpar(col = NA, fill = "#D2D200"))
for (y0 in seq(0, 1, len = 10)) {
  for (i in seq_along(px)) {
    th <- seq(pi/2, pi/2 + 2 * pi, len = 21)
    if (ag[i]%%2==0) th <- rev(th)
    x <- px[i] + 0.5 * 0.04 * cos(th) * wc[i]
    y <- y0 + 0.04 * sin(th)
    grid.polygon(x, y, gp = gpar(fill = "#3278FE"))
    grid.polyline(x[1:((dc + 1)/2)], y[1:((dc + 1)/2)], gp = gpar(lineend = "butt", lwd = 3, col = gray(0)))
    grid.polyline(x[-(1:((dc - 1)/2))], y[-(1:((dc - 1)/2))], gp = gpar(lineend = "butt", lwd = 3, col = gray(1)))
  }
}
</pre></div>
<div class="rimage default"><img src="figure/illusions_fraser_wilcox.png" title="plot of chunk illusions_fraser_wilcox" alt="plot of chunk illusions_fraser_wilcox" class="plot" /></div>
</div></div>


## Parallel curves ##
These curves are the same offset apart for every x, even though it looks like they converge.
<div class="chunk" id="illusions_parallel_lines"><div class="rcode"><div class="source"><pre class="knitr r">x=1:100
y=1/log10(x)
y2=y+.2
plot(x,y, type='l', ylim=c(0,1.5))
lines(x,y2)
</pre></div>
<div class="rimage default"><img src="figure/illusions_parallel_lines.png" title="plot of chunk illusions_parallel_lines" alt="plot of chunk illusions_parallel_lines" class="plot" /></div>
</div></div>

