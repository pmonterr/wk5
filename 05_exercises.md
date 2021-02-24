---
title: 'Weekly Exercises #5'
author: "Pablo Monterroso "
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
---





```r
library(tidyverse)     # for data cleaning and plotting
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
library(openintro)     # for the abbr2state() function
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
library(ggmap)         # for mapping points on maps
library(gplots)        # for col2hex() function
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 

# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)

# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")

panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")

panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")

#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  

```r
data(garden_harvest)
```


```r
warmup1 <- garden_harvest %>% 
  select(vegetable, variety) %>%
  filter( vegetable == "lettuce") %>%
  group_by(variety) %>% 
  summarize( count = n()) %>% 
  ggplot(aes(x = count,
             y = fct_reorder(variety, count))) +
  geom_col()+
  labs(title = "Amount of time different lettuce varieties were harvested",
       caption = "Data from: Lisa's Garden",
       y = "",
       x = "")

ggplotly(warmup1)
```

<!--html_preserve--><div id="htmlwidget-32ac6648195ad505ae20" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-32ac6648195ad505ae20">{"x":{"data":[{"orientation":"v","width":[27,29,1,3,9],"base":[3.55,4.55,0.55,1.55,2.55],"x":[13.5,14.5,0.5,1.5,4.5],"y":[0.9,0.9,0.9,0.9,0.9],"text":["count: 27<br />fct_reorder(variety, count): Farmer's Market Blend","count: 29<br />fct_reorder(variety, count): Lettuce Mixture","count:  1<br />fct_reorder(variety, count): mustard greens","count:  3<br />fct_reorder(variety, count): reseed","count:  9<br />fct_reorder(variety, count): Tatsoi"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(89,89,89,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":133.698630136986},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Amount of time different lettuce varieties were harvested","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-1.45,30.45],"tickmode":"array","ticktext":["0","10","20","30"],"tickvals":[0,10,20,30],"categoryorder":"array","categoryarray":["0","10","20","30"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,5.6],"tickmode":"array","ticktext":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"tickvals":[1,2,3,4,5],"categoryorder":"array","categoryarray":["mustard greens","reseed","Tatsoi","Farmer's Market Blend","Lettuce Mixture"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"ed9f4d324024":{"x":{},"y":{},"type":"bar"}},"cur_data":"ed9f4d324024","visdat":{"ed9f4d324024":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


```r
library(babynames)

bigbabyyyy <-babynames %>%
  group_by(year, sex) %>% 
  count() %>% 
  ggplot(aes(x=year, y=n, color=sex)) +
  geom_line() +
  labs(title = "Number of distinct names by sex between 1880-2017",
       caption = "Data is Lisa's kids favorite",
       y = "",
       x = "")

ggplotly(bigbabyyyy)
```

<!--html_preserve--><div id="htmlwidget-3359665e26722e636ffa" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-3359665e26722e636ffa">{"x":{"data":[{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[942,938,1028,1054,1172,1197,1282,1306,1474,1479,1534,1533,1661,1652,1702,1808,1825,1799,1975,1842,2224,1943,2042,2083,2165,2234,2220,2399,2434,2548,2790,2868,3445,3707,4206,4967,5162,5312,5586,5559,5765,5871,5789,5739,5899,5771,5621,5603,5436,5275,5248,4977,5100,4858,4973,4892,4856,4927,4994,4952,5025,5085,5380,5368,5245,5241,5686,6103,6040,6065,6111,6211,6391,6499,6616,6725,6885,7012,7022,7196,7331,7529,7583,7663,7803,7533,7616,7849,8194,8708,9350,9638,9661,9805,10239,10609,10900,11324,11470,11967,12157,12186,12327,12065,12171,12500,12823,13255,13877,14546,15235,15459,15611,15797,15751,15753,15891,16160,16598,16941,17653,17970,18081,18430,18826,19182,20050,20560,20457,20179,19811,19560,19498,19231,19181,19074,18817,18309],"text":["year: 1880<br />n:   942<br />sex: F","year: 1881<br />n:   938<br />sex: F","year: 1882<br />n:  1028<br />sex: F","year: 1883<br />n:  1054<br />sex: F","year: 1884<br />n:  1172<br />sex: F","year: 1885<br />n:  1197<br />sex: F","year: 1886<br />n:  1282<br />sex: F","year: 1887<br />n:  1306<br />sex: F","year: 1888<br />n:  1474<br />sex: F","year: 1889<br />n:  1479<br />sex: F","year: 1890<br />n:  1534<br />sex: F","year: 1891<br />n:  1533<br />sex: F","year: 1892<br />n:  1661<br />sex: F","year: 1893<br />n:  1652<br />sex: F","year: 1894<br />n:  1702<br />sex: F","year: 1895<br />n:  1808<br />sex: F","year: 1896<br />n:  1825<br />sex: F","year: 1897<br />n:  1799<br />sex: F","year: 1898<br />n:  1975<br />sex: F","year: 1899<br />n:  1842<br />sex: F","year: 1900<br />n:  2224<br />sex: F","year: 1901<br />n:  1943<br />sex: F","year: 1902<br />n:  2042<br />sex: F","year: 1903<br />n:  2083<br />sex: F","year: 1904<br />n:  2165<br />sex: F","year: 1905<br />n:  2234<br />sex: F","year: 1906<br />n:  2220<br />sex: F","year: 1907<br />n:  2399<br />sex: F","year: 1908<br />n:  2434<br />sex: F","year: 1909<br />n:  2548<br />sex: F","year: 1910<br />n:  2790<br />sex: F","year: 1911<br />n:  2868<br />sex: F","year: 1912<br />n:  3445<br />sex: F","year: 1913<br />n:  3707<br />sex: F","year: 1914<br />n:  4206<br />sex: F","year: 1915<br />n:  4967<br />sex: F","year: 1916<br />n:  5162<br />sex: F","year: 1917<br />n:  5312<br />sex: F","year: 1918<br />n:  5586<br />sex: F","year: 1919<br />n:  5559<br />sex: F","year: 1920<br />n:  5765<br />sex: F","year: 1921<br />n:  5871<br />sex: F","year: 1922<br />n:  5789<br />sex: F","year: 1923<br />n:  5739<br />sex: F","year: 1924<br />n:  5899<br />sex: F","year: 1925<br />n:  5771<br />sex: F","year: 1926<br />n:  5621<br />sex: F","year: 1927<br />n:  5603<br />sex: F","year: 1928<br />n:  5436<br />sex: F","year: 1929<br />n:  5275<br />sex: F","year: 1930<br />n:  5248<br />sex: F","year: 1931<br />n:  4977<br />sex: F","year: 1932<br />n:  5100<br />sex: F","year: 1933<br />n:  4858<br />sex: F","year: 1934<br />n:  4973<br />sex: F","year: 1935<br />n:  4892<br />sex: F","year: 1936<br />n:  4856<br />sex: F","year: 1937<br />n:  4927<br />sex: F","year: 1938<br />n:  4994<br />sex: F","year: 1939<br />n:  4952<br />sex: F","year: 1940<br />n:  5025<br />sex: F","year: 1941<br />n:  5085<br />sex: F","year: 1942<br />n:  5380<br />sex: F","year: 1943<br />n:  5368<br />sex: F","year: 1944<br />n:  5245<br />sex: F","year: 1945<br />n:  5241<br />sex: F","year: 1946<br />n:  5686<br />sex: F","year: 1947<br />n:  6103<br />sex: F","year: 1948<br />n:  6040<br />sex: F","year: 1949<br />n:  6065<br />sex: F","year: 1950<br />n:  6111<br />sex: F","year: 1951<br />n:  6211<br />sex: F","year: 1952<br />n:  6391<br />sex: F","year: 1953<br />n:  6499<br />sex: F","year: 1954<br />n:  6616<br />sex: F","year: 1955<br />n:  6725<br />sex: F","year: 1956<br />n:  6885<br />sex: F","year: 1957<br />n:  7012<br />sex: F","year: 1958<br />n:  7022<br />sex: F","year: 1959<br />n:  7196<br />sex: F","year: 1960<br />n:  7331<br />sex: F","year: 1961<br />n:  7529<br />sex: F","year: 1962<br />n:  7583<br />sex: F","year: 1963<br />n:  7663<br />sex: F","year: 1964<br />n:  7803<br />sex: F","year: 1965<br />n:  7533<br />sex: F","year: 1966<br />n:  7616<br />sex: F","year: 1967<br />n:  7849<br />sex: F","year: 1968<br />n:  8194<br />sex: F","year: 1969<br />n:  8708<br />sex: F","year: 1970<br />n:  9350<br />sex: F","year: 1971<br />n:  9638<br />sex: F","year: 1972<br />n:  9661<br />sex: F","year: 1973<br />n:  9805<br />sex: F","year: 1974<br />n: 10239<br />sex: F","year: 1975<br />n: 10609<br />sex: F","year: 1976<br />n: 10900<br />sex: F","year: 1977<br />n: 11324<br />sex: F","year: 1978<br />n: 11470<br />sex: F","year: 1979<br />n: 11967<br />sex: F","year: 1980<br />n: 12157<br />sex: F","year: 1981<br />n: 12186<br />sex: F","year: 1982<br />n: 12327<br />sex: F","year: 1983<br />n: 12065<br />sex: F","year: 1984<br />n: 12171<br />sex: F","year: 1985<br />n: 12500<br />sex: F","year: 1986<br />n: 12823<br />sex: F","year: 1987<br />n: 13255<br />sex: F","year: 1988<br />n: 13877<br />sex: F","year: 1989<br />n: 14546<br />sex: F","year: 1990<br />n: 15235<br />sex: F","year: 1991<br />n: 15459<br />sex: F","year: 1992<br />n: 15611<br />sex: F","year: 1993<br />n: 15797<br />sex: F","year: 1994<br />n: 15751<br />sex: F","year: 1995<br />n: 15753<br />sex: F","year: 1996<br />n: 15891<br />sex: F","year: 1997<br />n: 16160<br />sex: F","year: 1998<br />n: 16598<br />sex: F","year: 1999<br />n: 16941<br />sex: F","year: 2000<br />n: 17653<br />sex: F","year: 2001<br />n: 17970<br />sex: F","year: 2002<br />n: 18081<br />sex: F","year: 2003<br />n: 18430<br />sex: F","year: 2004<br />n: 18826<br />sex: F","year: 2005<br />n: 19182<br />sex: F","year: 2006<br />n: 20050<br />sex: F","year: 2007<br />n: 20560<br />sex: F","year: 2008<br />n: 20457<br />sex: F","year: 2009<br />n: 20179<br />sex: F","year: 2010<br />n: 19811<br />sex: F","year: 2011<br />n: 19560<br />sex: F","year: 2012<br />n: 19498<br />sex: F","year: 2013<br />n: 19231<br />sex: F","year: 2014<br />n: 19181<br />sex: F","year: 2015<br />n: 19074<br />sex: F","year: 2016<br />n: 18817<br />sex: F","year: 2017<br />n: 18309<br />sex: F"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)","dash":"solid"},"hoveron":"points","name":"F","legendgroup":"F","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1880,1881,1882,1883,1884,1885,1886,1887,1888,1889,1890,1891,1892,1893,1894,1895,1896,1897,1898,1899,1900,1901,1902,1903,1904,1905,1906,1907,1908,1909,1910,1911,1912,1913,1914,1915,1916,1917,1918,1919,1920,1921,1922,1923,1924,1925,1926,1927,1928,1929,1930,1931,1932,1933,1934,1935,1936,1937,1938,1939,1940,1941,1942,1943,1944,1945,1946,1947,1948,1949,1950,1951,1952,1953,1954,1955,1956,1957,1958,1959,1960,1961,1962,1963,1964,1965,1966,1967,1968,1969,1970,1971,1972,1973,1974,1975,1976,1977,1978,1979,1980,1981,1982,1983,1984,1985,1986,1987,1988,1989,1990,1991,1992,1993,1994,1995,1996,1997,1998,1999,2000,2001,2002,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012,2013,2014,2015,2016,2017],"y":[1058,997,1099,1030,1125,1097,1110,1067,1177,1111,1161,1127,1260,1179,1239,1241,1266,1229,1289,1200,1506,1210,1320,1306,1395,1421,1413,1549,1584,1679,1839,1999,2906,3261,3759,4390,4534,4602,4813,4810,4990,4986,4967,4904,4970,4867,4837,4803,4724,4543,4541,4320,4284,4154,4207,4145,4037,4019,4036,3967,3936,4000,4045,4040,3909,3783,4019,4268,4199,4203,4191,4251,4257,4339,4352,4388,4450,4552,4499,4573,4590,4652,4623,4619,4593,4420,4536,4550,4741,5040,5430,5655,5750,5876,6005,6335,6491,6851,6759,7071,7288,7286,7364,7338,7332,7581,7826,8148,8487,9227,9484,9646,9816,10169,10244,10327,10532,10811,11301,11609,12116,12299,12482,12753,13220,13364,14032,14390,14613,14523,14256,14343,14234,14038,14047,14024,14162,14160],"text":["year: 1880<br />n:  1058<br />sex: M","year: 1881<br />n:   997<br />sex: M","year: 1882<br />n:  1099<br />sex: M","year: 1883<br />n:  1030<br />sex: M","year: 1884<br />n:  1125<br />sex: M","year: 1885<br />n:  1097<br />sex: M","year: 1886<br />n:  1110<br />sex: M","year: 1887<br />n:  1067<br />sex: M","year: 1888<br />n:  1177<br />sex: M","year: 1889<br />n:  1111<br />sex: M","year: 1890<br />n:  1161<br />sex: M","year: 1891<br />n:  1127<br />sex: M","year: 1892<br />n:  1260<br />sex: M","year: 1893<br />n:  1179<br />sex: M","year: 1894<br />n:  1239<br />sex: M","year: 1895<br />n:  1241<br />sex: M","year: 1896<br />n:  1266<br />sex: M","year: 1897<br />n:  1229<br />sex: M","year: 1898<br />n:  1289<br />sex: M","year: 1899<br />n:  1200<br />sex: M","year: 1900<br />n:  1506<br />sex: M","year: 1901<br />n:  1210<br />sex: M","year: 1902<br />n:  1320<br />sex: M","year: 1903<br />n:  1306<br />sex: M","year: 1904<br />n:  1395<br />sex: M","year: 1905<br />n:  1421<br />sex: M","year: 1906<br />n:  1413<br />sex: M","year: 1907<br />n:  1549<br />sex: M","year: 1908<br />n:  1584<br />sex: M","year: 1909<br />n:  1679<br />sex: M","year: 1910<br />n:  1839<br />sex: M","year: 1911<br />n:  1999<br />sex: M","year: 1912<br />n:  2906<br />sex: M","year: 1913<br />n:  3261<br />sex: M","year: 1914<br />n:  3759<br />sex: M","year: 1915<br />n:  4390<br />sex: M","year: 1916<br />n:  4534<br />sex: M","year: 1917<br />n:  4602<br />sex: M","year: 1918<br />n:  4813<br />sex: M","year: 1919<br />n:  4810<br />sex: M","year: 1920<br />n:  4990<br />sex: M","year: 1921<br />n:  4986<br />sex: M","year: 1922<br />n:  4967<br />sex: M","year: 1923<br />n:  4904<br />sex: M","year: 1924<br />n:  4970<br />sex: M","year: 1925<br />n:  4867<br />sex: M","year: 1926<br />n:  4837<br />sex: M","year: 1927<br />n:  4803<br />sex: M","year: 1928<br />n:  4724<br />sex: M","year: 1929<br />n:  4543<br />sex: M","year: 1930<br />n:  4541<br />sex: M","year: 1931<br />n:  4320<br />sex: M","year: 1932<br />n:  4284<br />sex: M","year: 1933<br />n:  4154<br />sex: M","year: 1934<br />n:  4207<br />sex: M","year: 1935<br />n:  4145<br />sex: M","year: 1936<br />n:  4037<br />sex: M","year: 1937<br />n:  4019<br />sex: M","year: 1938<br />n:  4036<br />sex: M","year: 1939<br />n:  3967<br />sex: M","year: 1940<br />n:  3936<br />sex: M","year: 1941<br />n:  4000<br />sex: M","year: 1942<br />n:  4045<br />sex: M","year: 1943<br />n:  4040<br />sex: M","year: 1944<br />n:  3909<br />sex: M","year: 1945<br />n:  3783<br />sex: M","year: 1946<br />n:  4019<br />sex: M","year: 1947<br />n:  4268<br />sex: M","year: 1948<br />n:  4199<br />sex: M","year: 1949<br />n:  4203<br />sex: M","year: 1950<br />n:  4191<br />sex: M","year: 1951<br />n:  4251<br />sex: M","year: 1952<br />n:  4257<br />sex: M","year: 1953<br />n:  4339<br />sex: M","year: 1954<br />n:  4352<br />sex: M","year: 1955<br />n:  4388<br />sex: M","year: 1956<br />n:  4450<br />sex: M","year: 1957<br />n:  4552<br />sex: M","year: 1958<br />n:  4499<br />sex: M","year: 1959<br />n:  4573<br />sex: M","year: 1960<br />n:  4590<br />sex: M","year: 1961<br />n:  4652<br />sex: M","year: 1962<br />n:  4623<br />sex: M","year: 1963<br />n:  4619<br />sex: M","year: 1964<br />n:  4593<br />sex: M","year: 1965<br />n:  4420<br />sex: M","year: 1966<br />n:  4536<br />sex: M","year: 1967<br />n:  4550<br />sex: M","year: 1968<br />n:  4741<br />sex: M","year: 1969<br />n:  5040<br />sex: M","year: 1970<br />n:  5430<br />sex: M","year: 1971<br />n:  5655<br />sex: M","year: 1972<br />n:  5750<br />sex: M","year: 1973<br />n:  5876<br />sex: M","year: 1974<br />n:  6005<br />sex: M","year: 1975<br />n:  6335<br />sex: M","year: 1976<br />n:  6491<br />sex: M","year: 1977<br />n:  6851<br />sex: M","year: 1978<br />n:  6759<br />sex: M","year: 1979<br />n:  7071<br />sex: M","year: 1980<br />n:  7288<br />sex: M","year: 1981<br />n:  7286<br />sex: M","year: 1982<br />n:  7364<br />sex: M","year: 1983<br />n:  7338<br />sex: M","year: 1984<br />n:  7332<br />sex: M","year: 1985<br />n:  7581<br />sex: M","year: 1986<br />n:  7826<br />sex: M","year: 1987<br />n:  8148<br />sex: M","year: 1988<br />n:  8487<br />sex: M","year: 1989<br />n:  9227<br />sex: M","year: 1990<br />n:  9484<br />sex: M","year: 1991<br />n:  9646<br />sex: M","year: 1992<br />n:  9816<br />sex: M","year: 1993<br />n: 10169<br />sex: M","year: 1994<br />n: 10244<br />sex: M","year: 1995<br />n: 10327<br />sex: M","year: 1996<br />n: 10532<br />sex: M","year: 1997<br />n: 10811<br />sex: M","year: 1998<br />n: 11301<br />sex: M","year: 1999<br />n: 11609<br />sex: M","year: 2000<br />n: 12116<br />sex: M","year: 2001<br />n: 12299<br />sex: M","year: 2002<br />n: 12482<br />sex: M","year: 2003<br />n: 12753<br />sex: M","year: 2004<br />n: 13220<br />sex: M","year: 2005<br />n: 13364<br />sex: M","year: 2006<br />n: 14032<br />sex: M","year: 2007<br />n: 14390<br />sex: M","year: 2008<br />n: 14613<br />sex: M","year: 2009<br />n: 14523<br />sex: M","year: 2010<br />n: 14256<br />sex: M","year: 2011<br />n: 14343<br />sex: M","year: 2012<br />n: 14234<br />sex: M","year: 2013<br />n: 14038<br />sex: M","year: 2014<br />n: 14047<br />sex: M","year: 2015<br />n: 14024<br />sex: M","year: 2016<br />n: 14162<br />sex: M","year: 2017<br />n: 14160<br />sex: M"],"type":"scatter","mode":"lines","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)","dash":"solid"},"hoveron":"points","name":"M","legendgroup":"M","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":40.1826484018265},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Number of distinct names by sex between 1880-2017","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1873.15,2023.85],"tickmode":"array","ticktext":["1880","1920","1960","2000"],"tickvals":[1880,1920,1960,2000],"categoryorder":"array","categoryarray":["1880","1920","1960","2000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-43.1,21541.1],"tickmode":"array","ticktext":["0","5000","10000","15000","20000"],"tickvals":[-7.105427357601e-15,5000,10000,15000,20000],"categoryorder":"array","categoryarray":["0","5000","10000","15000","20000"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":true,"gridcolor":"rgba(235,235,235,1)","gridwidth":0.66417600664176,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"y":0.913385826771654},"annotations":[{"text":"sex","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"ed9f2a1c2b5d":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"ed9f2a1c2b5d","visdat":{"ed9f2a1c2b5d":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->


  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
arrivalz <-small_trains %>% 
  filter(arrival_station %in% c("Paris EST", "PARIS LYON", "PARIS MONTPARNASSE", "PARIS NORD", "Paris VAUGIRARD")) %>% 
  group_by(arrival_station, month) %>% 
  summarise(alltrips = sum(total_num_trips)) %>% 
  ggplot(aes(y=month, x=alltrips,
             color=arrival_station))+
  geom_line()+
  labs(title = "Arrivals in Paris train stations by month",
       y = "",
       x = "") +
  scale_fill_viridis_c()+
    transition_reveal(month)

animate(arrivalz, nframes = 100, duration = 10)
anim_save("arrivalz.gif")
```

## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
bigharvy <- garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0)) %>% 
  group_by(variety) %>% 
  mutate(cumsum = cumsum(daily_harvest_lb)) %>% 
  ggplot(aes(y = cumsum, x = date,
             fill = fct_reorder(variety, daily_harvest_lb))) +
  geom_area(position = "stack") +
  labs(fill = "Variety",
       title = "Cumulative pounds of tomato varieties harvested over time",
       x = "",
       y = "") +
  transition_reveal(date)

bigharvy

animate(bigharvy, nframes = 100, duration = 10)
anim_save("bigharvy.gif")
```


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  

```r
mallorca <- get_stamenmap(
  bbox = c(left = 2.28, bottom = 39.41, right = 3.03, top = 39.8),
  maptype = "terrain",
  zoom = 10
)

ggmap(mallorca) +
  geom_point(data = mallorca_bike_day7,
             aes(x = lon, y = lat),
             size = 2, color = "blue") +
  geom_path(data = mallorca_bike_day7,
            aes(x = lon, y = lat, color = ele),
            size = 0.5 ) +
  scale_color_viridis_c(option = "cyan") +
  theme_map() +
  theme(legend.background = element_blank()) +
  labs(title = "Bike Ride Through Mallorca",
       subtitle = "Time:{frame_along}",
       color = "Elevation") +
  annotate(geom = "text",
           x = 2.586255,
           y = 39.66033,
           label = "Start",
           color = "blue") +
  transition_reveal(time)

mallorca

animate(mallorca, nframes = 100, duration = 10)
anim_save("mallorca.gif")
```
  
   I prefer this map because it lets you know more about the bike journey and overall its a better visual.
 
 
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
panama <- get_stamenmap(
  bbox = c(left = -79.6, bottom = 8.9, right = -79.45, top = 9.0),
  maptype = "terrain",
  zoom = 14)
ironwoman <-bind_rows(panama_swim,panama_bike,panama_run)
ggmap(panama)+
  geom_path(data = ironwoman, 
            aes(x=lon, y=lat, color = event),
            size=1)+
  geom_point(data=ironwoman,
             aes(x=lon,y=lat, color=event),
             size=4)+
  labs(title = "Tracking Heather during Ironman",
       subtitle = "Time: {frame_along}",
       x="",
       y="",
       color= "Event")+
  theme_map()+
  theme(legend.background = element_blank())+
  transition_reveal(time)

ironwoman

anim_save("ironman.gif")
```
  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  

```r
covid <- covid19 %>% 
  group_by(state) %>% 
  mutate(one_day_lag= lag(cases, n=1),
         seven_day_lag= lag(cases, n=1)) %>% 
  replace_na(list(one_day_lag=0, seven_day_lag=0)) %>% 
  mutate(new_cases_1day= cases-one_day_lag) %>%
  mutate(new_cases_7day=cases-seven_day_lag) %>% 
  filter(cases>20) %>% 
  ggplot()+
  geom_path(aes(x=cases,y= new_cases_7day,group = state))+
  geom_point(aes(x=cases,y= new_cases_7day,group = state))+
  geom_text(aes(x=cases,y= new_cases_7day,group = state,label=state),check_overlap = TRUE)+
  scale_y_log10(labels=scales::comma)+
  scale_x_log10(labels=scales::comma)+
  labs(title = "Covid Cases",
       x="",
       y="",
       subtitle = "Date: {frame_along}")+
  transition_reveal(date)

covid 

animate(covid, nframes=200, duration = 30)
anim_save("covid.gif")
```

It seems that initially New York had significantly more cases but as time went on the other states caught up. In the last few months California, Florida, and Texas have has the most by a slight margin.


  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))

states_map <- map_data("state")
```


```r
case <- covid19 %>% 
  mutate(state_name = str_to_lower(state)) %>% 
  arrange(desc(date)) %>% 
  left_join(census_pop_est_2018,
            by = c("state_name" = "state")) %>% 
  mutate(cases_per_10000 = (cases/est_pop_2018)*10000,
         day_of_week = wday(date, label = TRUE)) %>% 
  filter(day_of_week == "Fri") %>% 
  ggplot()+
  geom_map(map=states_map,
           aes(map_id = state_name,
               fill = cases_per_10000,
               group = date))+
  expand_limits(x=states_map$long, y=states_map$lat)+ #for a nice visual
  theme_map()+
  labs(title="COVID-19 cases per 10,000 people in different states by color",
       fill = "Cases per 10,0000",
       subtitle = "Date: {frame_time}")+
  transition_time(date)

case

animate(case, nframes=200, end_pause=10)
anim_save("cases.gif")
```

This shows that most states had a similar rate of cases per capita. That being said it seems like the midwest initially started with the most cases and then it tapers of slightly towards the coasts.


## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.

https://github.com/pmonterr/wk5

**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
