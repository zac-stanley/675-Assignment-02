### 675-Assignment-02 - Lighting Types by Campus Regions - UC Berkeley
#### Proposed workflow:
1. Symbolize trails by type of path (dedicated vs. bicycle boulevard) - use this to create figure ground
2. Set 'Name' field to title case in QGIS because these will be used for tooltips in web map and should look the same (realized later this could have been done with ogr2ogr)
3. Filter dataset so only Albuquerque cartographic boundary is displayed
3. Verify that CRS on all datasets is 4326/WGS84
4. Convert all data to geoJSON
5. Create web map

#### Start Creating Files
1. Create *package.json* using `init npm`
2. Create *app.js* with `echo > app.js`
3. Create *index.html* with `echo > index.html`
    - Add boilder plate html, CSS and JavaScript to *index.html*
4. Create *project-files* directory and copy extracted shapefiles there


#### Review Data and simplify where necessary
1. Use mapshaper to inspect data with `mapshaper RegionsUCB.shp -info` and `mapshaper RLightingMergeUCBRegions.shp -info`
2. Project both files with mapshaper `mapshaper LightingMergeUCBRegions.shp -proj wgs84 -o RegionsUCB_WGS84.shp` and `mapshaper RegionsUCB.shp -proj wgs84 -o LightingUCB_WGS84.shp`
3. Create a geoJSON of lighting points, reducing the precision and removing some fields with `mapshaper LightingUCB_WGS84.shp -filter-fields POINT_X,POINT_Y,Region,ID,Abbrev -o precision=.01 format=geojson ../data/LightingUCB_WGS84.json`
4. Convert regions to geoJSON with `mapshaper RegionsUCB_WGS84.shp -o format=geojson ../data/RegionsUCB_WGS84.json`
    