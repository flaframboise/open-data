[In English](readme_en.md)

![ECCC logo](../img_eccc-logo.png)

[TdM](../readme_fr.md) > Aperçu de l'utilisation

# Aperçu de l'utilisation

Aperçu de l'utilisation et exemples pour accéder et utiliser les données ouvertes du Service météorologique du Canada.

[ RENDU ICI ]

* [Learn about the available data](#learn-about-the-available-data)
* [How to visualize the data](#how-to-visualize-the-data)
  * [Desktop software](#desktop-software)
  * [Interactive web maps and mobile apps](#interactive-web-maps-and-mobile-apps)
  * [On-the-fly images](#on-the-fly-images)
* [How to access raw data](#how-to-access-raw-data)
  * [Raw data download](#raw-data-download)
  * [Raw data web services](#raw-data-web-services)


## Learn about the available data

The Meteorological Service of Canada provides up-to-date information on past, present and future weather conditions, climate, water and environmental information over Canada and the world. [Details  on the available data is provided here](../msc-data/readme_en.md).

## How to visualize the data

### Desktop software 

MSC open data can be visualized in desktop software by either (A) connecting to MSC GeoMet Web Map Service (WMS) web services or (B) by downloading the raw data from MSC Datamart or MSC GeoMet Web Coverage Service (WCS) web services and loading the raw data in the application.

MSC open data can be interactively visualized in software that supports the OGC Web Map Service (WMS) standard such as the free and open source software [QGIS](https://qgis.org) and in Esri ArcGIS software. Instructions for adding [MSC GeoMet WMS services](../msc-geomet/readme_en.md) to [QGIS](https://docs.qgis.org/3.4/en/docs/training_manual/online_resources/wms.html) and [ArcGIS](https://desktop.arcgis.com/en/arcmap/latest/map/web-maps-and-services/adding-wms-services.htm) are available. Desktop software may allow users to change the layer colors (WMS styles) and animate the layers amongst the available timesteps. Details on the available WMS parameters are available in the [web services section](../msc-geomet/web-services.md).

For downloading raw data, refer to the [How to access raw data](#how-to-access-raw-data) section.


### Interactive web maps and mobile apps

MSC open data can also easily be integrated into interactive maps in browsers and mobile applications. 

#### In a web browser

By using JavaScript libraries such as [Leaflet](https://leafletjs.com/) and [Openlayers](https://openlayers.org/) (among others), users can integrate data available via MSC Geomet into their own interactive web maps.

Below is an example of an OpenLayers web map configured to display a radar composite Web Map Service (WMS) layer served by MSC GeoMet.

<div id="map" style="height: 400px"></div>

#### In a mobile application

MSC Geomet Web Map Services (WMS) can also be integrated into mobile applications. In fact, Environment and Climate Change Canada's [WeatherCAN application](https://www.canada.ca/en/environment-climate-change/services/weather-general-tools-resources/weathercan.html) (available on iOS and Android) uses GeoMet to display high resolution radar data on an interactive map:

![Example of radar imagery in WeatherCan](http://collaboration.cmc.ec.gc.ca/cmc/cmos/public_doc/usage/WeatherCAN_GeoMet_Radar_Hurricane_Michael_20181010_162830.png)

For additional information regarding the capabilities and parameters for MSC GeoMet web services (ie. WMS, WFS, WCS) refer to the [MSC GeoMet web services](../msc-geomet/web-services_en.md) documentation.

### On-the-fly images

MSC Geomet can also serve images on-the-fly via a WMS GetMap request. See the examples below.

#### Example 1 - Global Deterministic Prediction System (GDPS) Surface Temperature

The following GetMap request returns an image of the Global Deterministic Predicition System (GDPS) air temperature layer. The image is created "on-the-fly" at the time of the request.

```
https://geo.weather.gc.ca/geomet?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&BBOX=-90,-180,90,180
&CRS=EPSG:4326&WIDTH=600&HEIGHT=301&LAYERS=GDPS.ETA_TT&FORMAT=image/png
```
Returns:

![Global Deterministic Prediction System (GDPS) surface temperature](https://geo.weather.gc.ca/geomet?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&BBOX=-90,-180,90,180&CRS=EPSG:4326&WIDTH=600&HEIGHT=301&LAYERS=GDPS.ETA_TT&FORMAT=image/png)              

#### Example 2 - Global Ice Ocean Prediction System (GIOPS) Sea Water Salinity

The following GetMap request returns an image of the Global Ice Ocean Prediction System (GIOPS) sea water salinity layer. The image is created "on-the-fly" at the time of the request.
```
https://geo.weather.gc.ca/geomet?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&BBOX=-90,-180,90,180
&CRS=EPSG:4326&WIDTH=600&HEIGHT=301&LAYERS=OCEAN.GIOPS.2D_SALW&FORMAT=image/png
```
Returns:

![Sea Water Salinity from the Global Ice Ocean Prediction System (GIOPS) model](https://geo.weather.gc.ca/geomet?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&BBOX=-90,-180,90,180&CRS=EPSG:4326&WIDTH=600&HEIGHT=301&LAYERS=OCEAN.GIOPS.2D_SALW&FORMAT=image/png)

#### Short overview of WMS GetMap parameters used in the examples

The examples above define a handful of parameters and send a GetMap request to MSC GeoMet. Below is a short explanation of each parameter in the request:
* **SERVICE** - The name of the Open GeoSpatial Consortium Web Service to use in the request. In both examples, we are using the OGC Web Map Service (WMS).
* **VERSION** - The service version, in this case `1.3.0`.
* **REQUEST** - The specified request type. The WMS services specifies several different request types. In this case, we specify a GetMap request, which returns a map image.
* **BBOX** - The bounding box of the requested image. In our case, we are making a request for an image that covers the entire surface of the Earth. Coordinates are provided in the units of the Coordinate Reference System defined in the following parameter.
* **CRS** - The coordinate reference system (CRS) used to create the map image. In both examples, we set the CRS to `EPSG:4326` (e.g WGS 84), the coordinate reference system used for the Global Positioning System (GPS).
* **WIDTH** - The width in pixels of the returned image.
* **HEIGHT** - The height in pixels of the returned image.
* **LAYERS** - The name of the layer used to create the image. The name of the layer can be retrieved using a WMS GetCapabilities request.
* **FORMAT** - The format of the image returned by the GetMap request. In both cases case, the returned image will be in the PNG format. 

For further information regarding these and other WMS GetMap parameters, refer to the [MSC GeoMet web services](../msc-geomet/web-services_en.md) documentation.

## How to access raw data

### Raw data download

MSC data can be [automatically retrieved as soon as it becomes available through the Advanced Message Queuing Protocol (AMQP)](../msc-datamart/amqp_en.md).

The raw data can also be directly downloaded from the web on the MSC Datamart data repository.

### Raw data web services

Raw MSC data can be retrieved from the MSC GeoMet web services. These web services allow users to retrieve raw data by specifying the geographic coordinates, geographic projection, the temporal dimension and choose amongst available data formats. Details on the available parameters are provided in the [web services](../msc-geomet/web-services_en.md) section.

Raw data at specific geographic locations can be retrieved with a Web Map Service (WMS) GetFeatureInfo request. Example of a [WMS GetFeatureInfo request for temperature from the Global Deterministic Prediction System (GDPS) model over Montreal, Canada](https://geo.weather.gc.ca/geomet/?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetFeatureInfo&QUERY_LAYERS=GDPS.ETA_TT&INFO_FORMAT=text/plain&i=5&j=5&EXCEPTIONS=xml&LAYERS=GDPS.ETA_TT&CRS=EPSG:4326&BBOX=45.50,-73.56,45.51,-73.55&WIDTH=10&HEIGHT=10).

Raw data for vector data can be retrieved with a Web Feature Service (WFS) request. Example of a [WFS 3 query for the Winnipeg River hydrometric station daily means](https://geo.weather.gc.ca/geomet/features/collections/hydrometric-daily-mean/items?STATION_NUMBER=05PF049).

Raw data for raster data can be retrieved with a Web Coverage Service (WCS) request. Example of a [WCS 2 query for the Regional Deterministic Precipitation Analysis (RDPA) model in the netCDF format for a specific time](https://geo.weather.gc.ca/geomet?SERVICE=WCS&VERSION=2.0.1&REQUEST=GetCoverage&COVERAGEID=RDPA.6F_PR&SUBSETTINGCRS=EPSG:4326&FORMAT=image/netcdf&TIME=2019-05-14T12:00:00Z). A tip to build WCS queries is to use the [Canadian Centre for Climate Services WCS Query builder interface for an RDPA layer](https://climate-change.canada.ca/climate-data/#/regional-deterministic-precipitation-analysis) and replace the COVERAGEID value from RDPA.* to another available layer.

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.css" integrity="sha256-rQq4Fxpq3LlPQ8yP11i6Z2lAo82b6ACDgd35CKyNEBw=" crossorigin="anonymous" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/openlayers/4.6.5/ol.js" integrity="sha256-77IKwU93jwIX7zmgEBfYGHcmeO0Fx2MoWB/ooh9QkBA=" crossorigin="anonymous"></script>
<script type="text/javascript">
      var map = new ol.Map({
        target: 'map',
        layers: [
          new ol.layer.Tile({
            source: new ol.source.OSM()
          }),
          new ol.layer.Tile({
            source: new ol.source.TileWMS({
                format: 'image/png',
                url: 'http://geo.weather.gc.ca/geomet/',
                params: {'LAYERS': 'RADAR_1KM_RDBR', 'TILED': true},
            })
          })
        ],
        view: new ol.View({
          center: ol.proj.fromLonLat([-97, 44]),
          zoom: 3
        })
      });
</script>