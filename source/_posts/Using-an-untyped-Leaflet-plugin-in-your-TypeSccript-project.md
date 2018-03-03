title: Using an untyped Leaflet plugin in your TypeScript project
date: 2017-01-25
categories:
- GIS
tags:
- leaflet
-	typescript
---

[Leaflet](http://leafletjs.com/) has a prosperous ecosystem with [hundreds of plugins](http://leafletjs.com/plugins.html). Most of them are not typed for TypeScript, however, with a minimal setup, you are able to use these plugins in your TypeScript mapping project.

<!-- more -->

Since TypeScript is definitely typed, a simple workaround is to provide a minimal type declaration file that can expose the plugin functions in the `L` namespace.

For example, I would like to display a large GeoJSON file at the browser using the [vector tile](https://www.mapbox.com/vector-tiles/) technique. I can do it in JavaScript with the following code:

``` javascript
// Get the GeoJSON somewhere
let geojson = getGeoJSON();

// Slice the GeoJSON into vector tiles on-the-fly with L.vectorGrid.slicer()
let layer = L.vectorGrid.slicer(geojson, {});

// Add the tile layer on the map
layer.addTo(map);
```

The vector tile plugin [Leaflet.VectorGrid](https://github.com/Leaflet/Leaflet.VectorGrid) isn't officially typed and you are not able to directly use this plugin because the compiler doesn't know its existence. So we just need to declare it with a `leaflet.vectorgrid.d.ts` file

``` typescript
// in the global namesapce "L"
declare namespace L {

  // there is a child namespace "vectorGrid"
  namespace vectorGrid {

    // which has a function call "slicer" that takes data and optional
    // configurations. To make it simple, we don't specify the input
    // and output types.
    export function slicer(data: any, options?: any): any;
  }
}
```

Then we are able to use the function in TypeScript

``` typescript
/// <reference path="leaflet.vectorgrid.d.ts"/>

import 'leaflet';
import 'leaflet.vectorgrid';

let geojson = getGeoJSON();
let layer = L.vectorGrid.slicer(geojson)

layer.addTo(map);
```

Here we go!

If we want to use more, we could continue to populate the type declaration file and maybe contribute it to the community when it becomes more complete.

For a fully functional exampe, see [angular2-leaflet-starter](https://github.com/haoliangyu/angular2-leaflet-starter).
