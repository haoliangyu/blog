title: 'Boundary.Now: a simple tool to extract OSM place boundaries'
date: 2017-02-04 17:15:56
updated: 2017-02-26
categories:
- Project
tags:
- gis
- openstreetmap
---

Getting a place boundary is sometimes harder than it looks like.

<!-- more -->

There are a couple of reasons why it's hard:

* The boundary data is actually unavailable or not released.
* The boundary data is available, but packaged in a national dataset, like most governmental open data.
* The boundary data is visible, but not downloadable, like the Google map does.
* The boundary data is exportable, but the use is limited, like the Bing map geocoding API does.

So it's pretty common for a data analyst to take a lot of effort to find and extract place boundaries. It's even more painful when we have to download national datasets just for a few cities' boundary.

Oh, wait! Isn't it a free and global geospatial database out there?

Yeah, [OpenStreetMap](https://www.openstreetmap.org/) is awesome and the great [Nominatim](http://nominatim.openstreetmap.org/) service allows us to search through the OSM database with a place name.

The only problem is the Nominatim interface is not designed for data extraction, even though the API does return place boundary. So I develop [**Boundary.Now**](https://haoliangyu.github.io/boundary.now/), an interface for Nominatim geocoding API to download place boundary.

{% asset_img boundary-now.png This is an example image %}

Like the original interface, it will provide a search box for the desired place name. In the result list, only search results with boundary data are shown. The boundary data could be downloaded in **GeoJSON**, a format widely used in web development, or in **Shapefile**, a standard format in the GIS world.

You can open the tool [**here**](https://haoliangyu.github.io/boundary.now/) and the project is open at [GitHub](https://github.com/haoliangyu/boundary.now/).
