# Titanium Map Module [![Build Status](https://travis-ci.org/appcelerator-modules/ti.map.svg)](https://travis-ci.org/appcelerator-modules/ti.map)

This is the Map Module for Titanium. Please use [JIRA](http://jira.appcelerator.org) to report issues or ask our [TiSlack community](http://tislack.org) for help! :rocket:

This is a fork for supporting TileOverlays. 

<img src="https://raw.githubusercontent.com/AppWerft/ti.map/master/screens/Screenshot_20170219-112425.png" width=240 /><img src="https://raw.githubusercontent.com/AppWerft/ti.map/master/screens/Screenshot_20170219-112805.png" width=240 /><img src="https://raw.githubusercontent.com/AppWerft/ti.map/master/screens/Screenshot_20170219-114755.png" width=240 /><img src="https://raw.githubusercontent.com/AppWerft/ti.map/master/screens/Screenshot_20170219-115509.png" width=240 />


Screenshot_20170219-115509.png
##Usage
### Using of TileOverlays
```javascript
var map = require("ti.map");
var mapView = map.createView();
var weatherOverlay =  map.createTileOverlay({
    tileProvider : "OpenWeatherMap",
    variant : "RainClassic"
    opacity:0.7
});
mapView.addTileOverlay(weatherOverlay);
```
### Exploring database of TileProviders
For retreiving all possible variants of TileProviders and variants:
```javascript
var providerList = map.createTileProviderDatabase();
providerList.getAllProviders();  // gives list of all
var variants = providerList.getVariantsOfProvider("Stamen");  // gives list of all variants
console.log(variants);
// gives Toner, TonerBackground, TonerHybrid, TonerLines, TonerLabels, TonerLite, Watercolor
```

### Offline tiles

With the [Perl script](http://search.cpan.org/~rotkraut/Geo-OSM-Tiles-0.01/downloadosmtiles.pl) you can download all tiles from a region. This script generates folders and download all. After this you can use [mbutil](https://github.com/mapbox/mbutil/) for converting in mbtiles format. This sqlite format is basic for offline maps. Now you can call:
```javascript
var offlineOverlay =  map.createTileOverlay({
    tileProvider : Ti.Filesystem.getFile(Ti.Filesystem.applicationDataDirectory,"germany.mbtiles").nativePath,
});
mapView.addOverlay(offlineOverlay);
```

Because the offline Maps work with sqlite database you have to close the connection after map work:

```javascript
offlineOverlay.destroy();
```
This prevent memory leaks!

