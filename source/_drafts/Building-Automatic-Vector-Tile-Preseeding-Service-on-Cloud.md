title: Building Automatic Vector Tile Preseeding Service on Cloud
date: 2016-10-27
categories:
- Project
tags:
- gis
- OpenDataDiscovery.org
---

[OpenDataDiscovery.org](http://www.opendatadiscovery.org) publishes the status of open data portals every week therefore it needs a weekly update for its vector tile map. In this article, I will discuss how I set up the automatic vector tile preseeding service using AWS EC2 instances and Auto-Scaling service.

<!-- more -->

Before explaining the solution, I would like to briefly talk about the problem.

[OpenDataDiscovery.org](http://www.opendatadiscovery.org) currently has very low traffic and it merely requires a micro EC2 instance (1GB memory and 1-core CPU) to host both the server and the database.

Though it only takes 20 minutes, the tile preseeding is much more expensive and it needs a medium EC2 instance (4GB memory and 2-core CPU) to generate worldwide vector tile data.

My goal is to maintain a micro EC2 instance for hosting the website and only set up a medium EC2 instance when it's time to update map data. The whole procedure should be automatic and doesn't require human interwind. In this way, I can minimize my time and expense to maintain the service.

After reading the article [](), I decide to use AWS Auto-Scaling service to create instance for tile generation, which is able to self-initialize and self-destroy. With a proper estimation of the time required by tile generation, the procedure would include two steps:

1. the auto-scaling service sets up a medium
