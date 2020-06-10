# Correlation plot with histograms
This repo contains source code, supplementary files and pressentation for cool
correlation presentation of data.

For the purpose of following the workflow please choose `aronia_pomology.csv`

First you should import two functions

```
# Loading functions
panel.cor <- function(x, y, digits=2, prefix="", cex.cor, ...)
{
        usr <- par("usr"); on.exit(par(usr))
        par(usr = c(0, 1, 0, 1))
        r <- abs(cor(x, y))
        txt <- format(c(r, 0.123456789), digits=digits)[1]
        txt <- paste(prefix, txt, sep="")
        if(missing(cex.cor)) cex.cor <- 0.8/strwidth(txt)
        text(0.5, 0.5, txt, cex = cex.cor * r)
}

panel.hist <- function(x, ...)
{
        usr <- par("usr"); on.exit(par(usr))
        par(usr = c(usr[1:2], 0, 1.5) )
        h <- hist(x, plot = FALSE)
        breaks <- h$breaks; nB <- length(breaks)
        y <- h$counts; y <- y/max(y)
        rect(breaks[-nB], 0, breaks[-1], y, col = "cyan", ...)
}
```

Than you shoud load data set you want to correlate

```
# Choose dataset (aronia_pomology.csv)
df <- read.csv(file.choose(), header=TRUE)
```

Now print the chart
```
# Create chart
pairs(~H+X.Y+L+Wb+Wc+X.C+Y, data=df,
      lower.panel=panel.smooth, diag.panel=panel.hist, upper.panel=panel.cor, 
      pch=20, main="", labels = c("Height", "No.yng.s.", "Lenght yng.s.", 
                                  "Berry weight", "Cluster weight", 
                                  "No.clusters", "Yield")) 
```

Chart should look like this

![alt text](https://github.com/Shansh/pairs_panel_hist_plot/aronia_pomology.jpg?raw=true)

