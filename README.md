# Reproject US shapefiles to AlbersUsa composite projection for Tableau (or other slippy web maps)

This project contains an R function (toAlbersUsa) that performs a "dirty" reprojection of U.S. geographies to the [AlbersUsa composite projection](https://d3js.org/d3-geo/conic#geoAlbersUsa) for display on a web map (in web Mercator projection).

In the example provided (example.R) a shapefile of congressional districts from the Census Bureau is reprojected to a composite file that can simply be loaded into a web map application such as Tableau or Mapbox Studio. Note that the reprojected data will not appear in the "correct" location on the web map, so Tableau background layers should be disabled and any other layers you wish to display must also be reprojected.

Does not currently support data that includes Puerto Rico or outlying territories.