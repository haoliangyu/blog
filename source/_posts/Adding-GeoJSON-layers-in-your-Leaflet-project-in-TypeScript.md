title: Adding GeoJSON layers to your Leaflet map in TypeScript
date: 2017-02-04 00:53:35
categories:
- GIS
tags:
- geojson
- leaflet
-	typescript
---

Adding a GeoJSON layer to a [Leaflet](http://leafletjs.com/) map in [TypeScript](http://www.typescriptlang.org/) has some difference from that in JavaScript.

<!-- more -->

 It's because the GeoJSON is typed in TypeScript and the type declaration of Leaflet adopts it. So whenever you construct the GeoJSON object in TypeScript, it's important to declare the type of the variable as GeoJSON type:

 ``` typescript
// it's necessary to tell variable type
let featureCollection: GeoJSON.FeatureCollection<any> = {
  type: 'FeatureCollection',
  features: [
    {
      type: 'Feature',
      geometry: {
        type: 'Point',
        coordinates: [0, 0]
      },
      properties: {}
    }
  ]
};

// the Leaflet API is the same as the JavaScript one, except for the parameter type requirement
L.geoJSON(featureCollection).addTo(this.map);
```

For more about the specification and example, take a look at the [GeoJSON type definition](https://github.com/DefinitelyTyped/DefinitelyTyped/tree/master/geojson).
