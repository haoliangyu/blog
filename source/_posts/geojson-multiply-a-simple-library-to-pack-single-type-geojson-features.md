title: 'geojson-multiply: a simple package to pack single tyle geojson features'
date: 2016-05-07
comments: true
categories:
- GIS
tags:
- javascript
- geojson
---

Some PostGIS functions only accept multi type geometry, so I write a simple geojson utility package to help me aggregate geojson features.

<!-- more -->

The basic purpose of `geojson-multiply` is to generate a `MutliPoint`/`MultiLineString`/`MultiPolygon` geojson feature from many `Point`/`LineString`/`Polygon` geojson features. So this package provides a function

```
multiply(geojsons[, options])
```

Where the `geojsons` could be a geojson feature, an array of geojson features, or a geojson feature collection

Not just the coordinates, the `multiply()` also supports the aggregation of properties. Its `options` parameter accepts two input:

* `properties` - the default properties of result geojson

* `onEachFeature` - a function to aggregate properties. It has four parameters:

  * `properties` - the result geojson's properties

  * `featureProp` - input feature geojson's properties

  * `index` - input feature geojson's index in the array

  * `geojsons` - geojson array.

It takes the form of [Array.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) and make the aggregation pretty straightforward:

```javascript
var multiply = require('geojson-multiply');

var geojsonA = {
  type: 'Feature',
  geometry: { type: 'Point', coordinates: [12, 43] },
  properties: { count: 5 }
};

var geojsonB = {
  type: 'Feature',
  geometry: { type: 'Point', coordinates: [13, 34] },
  properties: { count: 5 }
};

var onEachFeature = function(properties, featureProp) {
  properties.count += featureProp.count;
  return properties;
};

var result = multiply([geojsonA, geojsonB], {
  properties: { count: 0 },
  onEachFeature: onEachFeature
});

/**
The reuslt geojson should be
{
  type: 'Feature'
  geometry: {
    type: 'MultiPoint',
    coordinates: [[12, 43], [14, 34]]
  },
  properties: {
    count: 10
  }
}
*/
```

This package has been published at [npm](https://www.npmjs.com/package/geojson-multiply). If you think it's helpful, just install and try!

```
npm install geojson-multiply --save
```
