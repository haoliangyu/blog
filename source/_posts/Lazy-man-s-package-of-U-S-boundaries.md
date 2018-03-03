title: Lazy man's package of nationwide U.S. boundaries
date: 2015-12-05
updated: 2016-01-24
categories:
- GIS
tags:
- gis
-	open data
---

I have been doing GIS work for quite a while and I do hate to download data from multiple sites every time. So I decide to collect those commonly geospatial data and make my own database. Of course, like all open-source people do, I'd love to share my work with you. The first release is the U.S. nationwide U.S. boundary. This dataset include **nation**, **state**, **county**, **place**, **census block**, and **census tract**. The source data come from U.S. Census Bureau and you can find the metadata [here](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html).

Multiple formats provided: **shapefile**, **geojson**, and a **postgis** database dump.<!-- more -->

shapefile/geojson
-----------------

| Resolution   | 1:500,000                                                             | 1:5,000,000                                                           | 1:20,000,000                                                          |
|--------------|-----------------------------------------------------------------------|-----------------------------------------------------------------------|-----------------------------------------------------------------------|
| Nation       |                                                                       | [Shapefile](http://1drv.ms/1Q7B59y)/[GeoJson](http://1drv.ms/1Q7Bgln) | [Shapefile](http://1drv.ms/1OaB9j0)/[GeoJson](http://1drv.ms/1Q7BhFR) |
| State        | [Shapefile](http://1drv.ms/1OaBfqW)/[GeoJson](http://1drv.ms/1XKAjUs) | [Shapefile](http://1drv.ms/1XKAaAg)/[GeoJson](http://1drv.ms/1XKAmzF) | [Shapefile](http://1drv.ms/1XKAcsb)/[GeoJson](http://1drv.ms/1XKAu25) |
| County       | [Shapefile](http://1drv.ms/1YR7XVF)/[GeoJson](http://1drv.ms/1XKAjUs) | [Shapefile](http://1drv.ms/1YR81EY)/[GeoJson](http://1drv.ms/1XKAmzF) | [Shapefile](http://1drv.ms/1YR82sq)/[GeoJson](http://1drv.ms/1XKAu25) |
| Census Tract | [Shapefile](http://1drv.ms/1TsP5Zm)/[GeoJson](http://1drv.ms/1TsPf2U) |                                                                       |                                                                       |
| Census Block | [Shapefile](http://1drv.ms/1TsPafL)/[GeoJson](http://1drv.ms/1TsP9s6) |                                                                       |                                                                       |
| Place        | [Shapefile](http://1drv.ms/1jViGyB)/[GeoJson](http://1drv.ms/1jViD63) |                                                                       |                                                                       |

postgis
-------

Download [U.S. boundary database](http://1drv.ms/1JtYaSe)

The data links are also at [GitHub](https://github.com/haoliangyu/us-boundary).

Ok, enjoy the data :)
