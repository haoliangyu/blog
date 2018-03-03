title: The Launch of OpenDataDiscovery.org
date: 2016-10-10
comments: true
categories:
- GIS
tags:
- open data
- gis
- OpenDataDiscovery.org
---

After several months' work at my spare time, I finally publish the first version of my side-project [OpenDataDiscovery.org](http://opendatadiscovery.org/). It is a step to answer this very simple question in my mind: **How many open datasets do we have on earth?**

<!-- more -->

I don't remember exactly when I started thinking about this question. It seems to be natural to ask, but very easy to ignore at the era of open data blooming.

Just look around. Every people, every government, every institute is talking about open data and releasing their data. EPA, NOAA, NOAA, and many other research institutes provide similar data from different angles about the same aspect of air pollution. Both USGS and USDA publish their soil survey. Numerous federal and local agencies are building their own data portals. Not to mention many research institutes have been doing that for years.

The rapidly increasing number of data providers and open data creates a view of prosperity, which is going to create another problem: we are walking out of the data desert and now into a data jungle. When the available data is not as much as today, figuring out what and how data are published is not very difficult as there is a small market. However, within a data jungle, it may be easy to understand the status of data opening at the domain you are familiar with, but difficult to look beyond. It is not just because increasing open data brings increasing information, but there are more things happening outside our individual's knowledge. We tend to be lost in the numerous options of data and miss the whole picture.

Therefore, when I try to answer my initial question, I know there is a lot data at anywhere but cannot figure out even an estimate.

The methodology to answer this question is not complex. I just need to collect information from all data portals and create the overview of the world of open data. The difficult part is `all data portals`. Fortunately, in the open data industry, there are dominant data portal platform providers, who are willing to open the API for data harvesting. These open API allows developers to collect rich information from each individual portal based on their platform, including dataset number, tag, category, publisher etc.

All I need is a program that could help me automatically collect information from related portals and provide a summary view. So I develop the application [OpenDataDiscovery.org](http://opendatadiscovery.org/), which runs the server for data collection and presents the map view of all data portals on earth.

Today the OpenDataDiscovery.org has been up and running. It is collecting information for more than 100 CKAN instances ([see the list](http://ckan.org/instances/)) and presents the status for these portals. As it update in a weekly basis, it is able to keep track of the status of worldwide data opening.

{% asset_img map.png This is an example image %}


Like a puzzle game, it needs us to put every piece into the frame in order to retrieve the overall view. By continuously adding portals into OpenDataDiscovery.org, it will eventually present a full and live picture of the world of open data. Let's see!
