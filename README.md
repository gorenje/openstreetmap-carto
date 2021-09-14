# OpenStreetMap Carto

**This version generates a black/white map of Berlin metro area.**

![screenshot](https://raw.github.com/gorenje/openstreetmap-carto/berlin_black_white/preview.png)

The following is taken from [Docker installation instructions](https://github.com/gravitystorm/openstreetmap-carto/blob/master/DOCKER.md) and applied to this repo.

## Quick start

If you are eager to get started here is an overview over the necessary steps.
Read on below to get the details.

* `git clone https://github.com/gorenje/openstreetmap-carto.git` to clone openstreetmap-carto repository into a directory on your host system
* checkout the berlin black & white branch: `cd openstreetmap-carto && git checkout berlin_black_white`
* download OpenStreetMap data in osm.pbf format to a file `data.osm.pbf` and place it within the openstreetmap-carto directory. for this step, use the European -> Germany -> Brandenburg with Berlin data from [Geofabrik](https://download.geofabrik.de/) or [direct link download link](https://download.geofabrik.de/europe/germany/brandenburg-latest.osm.pbf)
* If necessary, `sudo service postgresql stop` to make sure you don't have currently running a native PostgreSQL server which would conflict with Docker's PostgreSQL server.
* `docker-compose up import` to import the data (only necessary the first time or when you change the data file)
* `docker-compose up kosmtik` to run the style preview application
* browse to [http://localhost:6789](http://localhost:6789) to view the output of Kosmtik
* Ctrl+C to stop the style preview application
* `docker-compose stop db` to stop the database container

## Generating tiles

* To dump the tiles, first create a directory to store those tiles (ca. 1.5GB required). Then edit the [docker-compose.yml](https://github.com/gorenje/openstreetmap-carto/blob/berlin_black_white/docker-compose.yml#L15) and change the volume line `- /mnt/backup02/tiles:/openstreetmap-carto/tmp2` to put to your directory (i.e. `/mnt/backup02/tiles` needs changing).
* Then trigger the tile generating: `docker-compose up generate-tiles`


## Tile usage

These tiles can then be used instead of a OSM link, for example [like this](https://github.com/gorenje/urban-photogrammetry.org/blob/a250f558f384dfd889b0b7ac312d69ade81a626f/f/maphelper.js#L227). For the following [end result](https://urban-photogrammetry.org/berlin/maptour).
