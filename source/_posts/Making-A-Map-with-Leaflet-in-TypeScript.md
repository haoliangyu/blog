title: Making Map with Leaflet in TypeScript
date: 2016-05-06
update: 2016-12-27
categories:
- GIS
tags:
- leaflet
-	typescript
---

**UPDATE 27/12/2016**: update for TypeScript 2.0

Recently I am working on a web mapping project based on [Angular 2](https://angular.io/). There isn't much data on how to create web map using [Leaflet](http://leafletjs.com/) in TypeScript. So I think it's good to write a post on it.

<!-- more -->

### Leaflet, Typed

TypeScript is definitely typed so you need to provide a type declaration for Leaflet first. The installation of type declaration is much easier at TypeScript 2.0 for its direct support of [npm](https://www.npmjs.com/) and you just needs

``` bash
/**
 * Type declaration for GeoJSON, a dependency
 */

npm install @types/geojson

/**
 * Type declaration for Leaflet
 */

npm install @types/leaflet
```

It will download the type declaration publish [DefinitelyTyped](http://definitelytyped.org/) and relate to the installed package. Simple and no more package manager!

### Mapping

Using Leaflet in TypeScript doesn't have an essential difference with using it in JavaScript. The only difference is, in the typed environment, many things are declared as class. So you may need to new a class before directly using it:

``` javascript
let map = new L.Map('map', {
  center: new L.LatLng(40.731253, -73.996139),
  zoom: 12,
});
```

Also you will need to provide extra type information when using function:

``` javascript
map.on('click', (e: LeafletMouseEvent) => {
  let marker = L.marker(e.latlng)
  .bindPopup('Popup')
  .addTo(map)
  .openPopup();
});
```

And that's it. You should have no extra difficult in using Leaflet in TypeScript, if you are familiar with using it in JavaScript and has read the type declaration on what you need.

Hope you enjoy the journey with TypeScript :)
