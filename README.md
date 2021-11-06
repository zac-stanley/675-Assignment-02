### 675-Assignment-02 - Lighting Types by Campus Regions - UC Berkeley
#### Proposed workflow:
1. Symbolize trails by type of path (dedicated vs. bicycle boulevard) - use this to create figure ground
2. Set 'Name' field to title case in QGIS because these will be used for tooltips in web map and should look the same (realized later this could have been done with ogr2ogr)
3. Filter dataset so only Albuquerque cartographic boundary is displayed
3. Verify that CRS on all datasets is 4326/WGS84
4. Convert all data to geoJSON
5. Create web map

#### Create Files and Install Packages
1. Create *package.json* using `npm init`
2. Create *app.js* with `echo > app.js`
3. Install chalk `npm install chalk --save`
4. Install csv2geojson `npm install csv2geojson`
4. Create *index.html* with `echo > index.html`
    - Add boilder plate html, CSS and JavaScript to *index.html*
5. Create *project-files* directory 

#### Parsing, Inspecting, Filtering and Converting Data
1. Convert *lighting-ucb.csv* to json with `node csv2json.js`
2. Filter data and remove columns with `node csv2json-filtered.js` onlye keep keeping 'Region' and 'ID' fields
3. Use mapshaper to inspect data with regions polygon shapefile `mapshaper RegionsUCB.shp -info` it's in CRS NAD83 State Plane Zone3
4. Project file with mapshaper `mapshaper RegionsUCB.shp -proj wgs84 -o RegionsUCB_WGS84.shp`
5. Convert *RegionsUCB_WGS84.shp* to geoJSON with `mapshaper RegionsUCB_WGS84.shp -o format=geojson ../data/regions-ucb-wgs84.json`
6. Inspect output with:
    - `mapshaper ../data/RegionsUCB_WGS84.json -info`
    [info]
    ===============================
    Layer:    RegionsUCB_WGS84
    -------------------------------
    Type:     polygon
    Records:  6
    Bounds:   -122.26855683451866,37.86700095038925,-122.25233281442081,37.87625001480479
    CRS:      +proj=longlat +datum=WGS84
    Source:   ../data/RegionsUCB_WGS84.json

    Attribute data
    ------------+------------------
    Field      | First value
    ------------+------------------
    Region     | 'Region 5'
    Shape_Area | 1800889.11037
    Shape_Leng |    8503.75566012
    ------------+------------------

#### Web Mapping
1. Load boilerplate HTML, CSS and JaveScript
2. Update the Leaflet map origin 

```js
  center: [37.8719, -122.2585],
  zoom: 16
```
