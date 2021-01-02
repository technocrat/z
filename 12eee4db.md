---
date: 2021-01-02T17:15
---

# AK HI insets

[[[GIS]]]
[[R]]
[[script]]

```r
x <- c("acs","ggplot2", "dplyr","rgdal", "maptools", "mapproj", "rgeos")
lapply(x, library, character.only = TRUE)
load('data/cd114')
us <- cd114
# CRS to go back to after tweaks to inset
saveproj <- us@proj4string
us_aea <- spTransform(us, CRS("+proj=laea +lat_0=45 +lon_0=-100 +x_0=0 +y_0=0 +a=6370997 +b=6370997 +units=m +no_defs"))
us_aea@data$id <- rownames(us_aea@data)

alaska <- us_aea[us_aea$STATEFP=="02",]
alaska <- elide(alaska, rotate=-50)
alaska <- elide(alaska, scale=max(apply(bbox(alaska), 1, diff)) / 2.3)
alaska <- elide(alaska, shift=c(-2100000, -2500000))
proj4string(alaska) <- proj4string(us_aea)

hawaii <- us_aea[us_aea$STATEFP=="15",]
hawaii <- elide(hawaii, rotate=-35)
hawaii <- elide(hawaii, shift=c(5400000, -1400000))
proj4string(hawaii) <- proj4string(us_aea)

us_aea <- us_aea[!us_aea$STATEFP %in% c("02", "15","60","66","69","72","78"),]
us_aea <- rbind(us_aea, alaska, hawaii)
# retransform to long/lat
us50 <- spTransform(us_aea, saveproj)
map <- fortify(us50, region="GEOID")
b = ggplot(data= map) + 
	geom_map(map=map, aes(x=long, y=lat, map_id=id, group=group),fill="white", color="black", size=0.3)
district <- geo.make(state = "*", congressional.district="*")
ethnicity <- c("B03002_001","B03002_003")
ethnic.acs <- acs.fetch(geo=district, variable = c("B03002_001","B03002_003"), endyear = 2013) #ignore spurious warning
ethnic.df <- as.data.frame(estimate(ethnic.acs))
names(ethnic.df) <- c("total", "white")
# get rid of PR
ethnic.df <- filter(ethnic.df, row_number() != n())
# after much hand work
load('Rda/congress.Rda')
colnames(congress)[8] <- 'id'
map <- merge(map, congress)
defactor <- function(x) {as.numeric(levels(x))[x]}
b <- ggplot() + geom_polygon(data = map, aes(x=long, y=lat, group=group, fill = mbin), color = "dark grey", size = 0.3) 
b h
a <- ggplot() + geom_polygon(data = map, aes(x=long, y=lat, group=group, fill = "light grey"), color = "dark grey", size = 0.3) 
c <- ggplot() + geom_polygon(data = wbhmap, aes(x=long, y=lat, group=group, fill = rdsbin), color = "dark grey", size = 0.3) 

c + scale_fill_brewer(type = "div", palette = "RdBu") +  plain_theme + no_xlab + no_ylab + coord_map("polyconic") 

+ geom_point(data = wbh, colour="black", size = 3, alpha = 0.5, aes(x=lon,y=lat)) + geom_point(data = deaths, colour="yellow", size = 1.5, aes(x=lon,y=lat)) 




b + geom_point(data = wudeaths, colour="grey", size = 1.5, aes(x=lon,y=lat)) + geom_point(data = mudeaths, colour="red", size = 1.5, aes(x=lon,y=lat)) 
+ geom_point(data = budeaths, colour="black", size = 1.5, aes(x=lon,y=lat)) + geom_point(data = hudeaths, color = "yellow", size = 1.5, aes(x=lon,y=lat))
 
coordinates(locs) <- c("lon","lat")
proj4string(locs) <- proj4string(cd114)
inside.cd <- !is.na(over(locs, as(cd114, "SpatialPolygons")))
inside.cd
```