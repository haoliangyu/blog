title: 'gtran: a promised, consistent, user-friendly GeoJson conversion package'
date: 2016-02-25
comments: true
categories:
- Project
tags:
- gis
- project
- javascript
---

Do you still feel inconvenient when converting GeoJson to other data formats in Node.js?

<!-- more -->

GeoJson is one of simplest geographic data format. If we search for data conversion packages at [npm.org](https://www.npmjs.com/), there will be a long list packages: [shapefile](https://www.npmjs.com/package/shapefile) for shapefile, [tokml](https://www.npmjs.com/package/tokml) for kml, [geojson2dcsv](https://www.npmjs.com/package/geojson2dsv) for csv, [osm-and-geojson](https://www.npmjs.com/package/osm-and-geojson) for osm package, [geojson2](https://www.npmjs.com/package/geojson2) for multiple formats, [org2org](https://www.npmjs.com/package/ogr2ogr) and [gdal](https://www.npmjs.com/package/gdal) as data solutions... However, I still felt very inconvenient when I developed a GeoJson handling module a few months ago.

# Why inconvenient?

From my point of view, there are a few problems:

* Most packages are designed for one specific data format.

* Each package is written in a style different from the other.

* Some packages require external libraries,like [gdal](http://www.gdal.org/), which aren't npm-able.

* Most package aren't asynchronous or promised. (maybe just a personal problem)

As a result, in order to make them work together, one will need to learn how to use these diverse packages, customize code to handle their diverse input/output, and write some comments for the future project maintainer.

Well, it's not very fun.

# Gtran: the solution

The programmer's way to handle unhappiness is to write something that make him happy :) What I want is a package with following features:

* Able to work with multiple formats

* Consistent and simple: functions and their input/output

* Completely npm-able

* Asynchronous

And here comes **[gtran](https://www.npmjs.com/package/gtran)**.

# What does gtran do?

**gtran** wraps several existing npm packages to provide

* from/to conversion of multiple formats: .shp, .kml, .kmz, .csv, and TopoJson.

* consistent functions: from\[format name\]() and to\[format name\]()

* simple input/output: geojson or file name

* asynchronous ability with your favorite promise library ([bluebird](https://www.npmjs.com/package/bluebird), [promise](https://www.npmjs.com/package/promise), [Q](https://www.npmjs.com/package/q), or [native](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)).

* minimal installation: each format support is provide by a child package gtran-xxx.

It could be installed with `npm install gtran`.

# How could it be used?

A complete use guide could be found at the [GitHub repo](https://github.com/haoliangyu/gtran) and here is a small use case:

``` JavaScript
var gtran = require('gtran');

# Specify the promise library if necessary
gtran.setPromiseLib(require('bluebird'));

# Read shapefile
gtran.fromShp('source.shp')
.then(function(object) {
    var geojson = object;
});

# Save geojson into shapefile
gtran.toShp(geojson, 'point.shp')
.then(function(fileNames) {
    console.log('SHP files have been saved at:' + fileNames.toString());
});

# Read csv file
# Assume the test.csv has two columns: latitude and longitude
gtran.fromCSV('source.csv', {
    mapping: { x: 'longitude', y: 'latitude' }
})
.then(function(object) {
    var geojson = object;
});

# Save geojson into a csv file
gtran.toCSV(geojson, 'point.csv')
.then(function(fileName) {
    console.log('CSV file has been saved at:' + fileName);
});
```

Hope you enjoy it. If you find a bug or want a new feature, just create an [issue](https://github.com/haoliangyu/gtran/issues) and I will appreciate it :-)
