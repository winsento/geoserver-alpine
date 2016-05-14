# Supported tags and respective `Dockerfile` links #

- [`2.8.3`, `2.8`, `latest` (*2.8/Dockerfile*)](/src/default/2.8)

[![](https://badge.imagelayers.io/winsent/geoserver-alpine:latest.svg)](https://imagelayers.io/?images=winsent/geoserver-alpine:latest)

# What is GeoServer? #
GeoServer is a Java-based software server that allows users to view and edit geospatial data. Using open standards set forth by the [Open Geospatial Consortium (OGC)](http://www.opengeospatial.org/), GeoServer allows for great flexibility in map creation and data sharing.

![GeoServer_200.png](http://static.geoserver.org/images/GeoServer_200.png)

wiki: [wikipedia.org](https://wikipedia.org/wiki/GeoServer) | site: [geoserver.org](http://geoserver.org/) | documentation: [docs.geoserver.org](http://docs.geoserver.org/) | repository: [github.com](https://github.com/geoserver/geoserver)
# Image description #

Is not official GeoServer image based on [Alpine-Java](https://hub.docker.com/r/anapsix/alpine-java/) container (image size **447.5 MB**) with `JAI 1.1.3`, `ImageIO 1.1`, `GDAL 1.11.4` and extensions:

* ogr
* gdal
* printing
* importer


# How to use this image #
## Start a GeoServer instance ##

```console
$ docker run -d winsent/geoserver

```
You can test it by visiting http://container-ip:8080

## Using a custom GeoServer data directory ##
Make geoserver data directory and run container
```console
$ mkdir /data/geoserver_data
$ docker run --name geoserver --restart=always -d -p 8080:8080 -v /data/geoserver_data:/opt/geoserver/data_dir winsent/geoserver-alpine

```

## License ##
GeoServer licensed under the [GPL](http://www.gnu.org/licenses/old-licenses/gpl-2.0.html).

# Other GIS containers

* Geoserver on Ubuntu ([link](https://hub.docker.com/r/winsent/geoserver/))
* OSM tools ([link](https://hub.docker.com/r/cartography/osmtools/))
* Nominatim ([link](https://hub.docker.com/r/cartography/nominatim-docker/))
* OSRM backend ([link](https://hub.docker.com/r/cartography/osrm-backend-docker/))
* OSRM frontend ([link](https://hub.docker.com/r/cartography/osrm-frontend-docker/))

# User Feedback

## Issues

If you have any problems or questions about this image, please contact me through a [Bitbucket issue](https://bitbucket.org/ololoteam/geoserver-docker/issues) or email [pipetc@gmail.com](mailto:pipetc@gmail.com).