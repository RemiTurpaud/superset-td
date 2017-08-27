# Superset & Teradata
[Superset](https://github.com/apache/incubator-superset) docker image with Teradata database drivers. 
Uses the [Teradata Dialect for SQL Alchemy](https://github.com/Teradata/sqlalchemy-teradata). 

## Image build
* Download this repository
* Download the [Teradata ODBC Drivers for Linux](http://downloads.teradata.com/download/connectivity/odbc-driver/linux) (you will need to register and accept the licnce terms). And place the tar.gz file in this folder.
* Optional: Edit the defaults for [application configuration options](superset.cfg) or [admin credentials](admin.cfg). These files will be used to setup application and create backend if no persistent superset config is found.
* Build the image from this folder: 
`docker build -t superset-td .`

## Express setup
By default, this image will setup a local Superset application and database backend at runtime, using its default [application](superset.cfg) and [admin](admin.cfg) settings.
This of course implies that any changes made will be lost with the container, but this is good enough to get test the image. 

`run -d --name superset-td -p 8088:8088 superset-td`

## Backend Persistance
To persist the backend and application configuration, map a volume to the /superset point.
If not found, the default Superset application and database backend will be deployed to this volume.

`docker run -it --name superset-td   -v /tmp/superset:/superset:z   -p 8088:8088 superset-td`

## Getting started