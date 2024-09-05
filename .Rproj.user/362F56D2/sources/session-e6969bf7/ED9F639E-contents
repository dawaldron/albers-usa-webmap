toAlbersUsa <- function(infile, outfile) {
  require(sf)

  
  # read file
  sf_in <- st_read(infile)
  
  
  # transform to wgs84
  sf_wgs84 <- st_transform(sf_in, 4326)
  
  
  # select features in Alaska area and transform
  bbox.ak1 <- c(xmin = 171.2, ymin = 50.9, xmax = 180, ymax = 72.8)
  class(bbox.ak1) <- 'bbox'
  sf_bbox.ak1 <- st_as_sfc(bbox.ak1) |>
    st_set_crs(st_crs(sf_wgs84))
  
  bbox.ak2 <- c(xmin = -180, ymin = 50.9, xmax = -128.6, ymax = 72.8)
  class(bbox.ak2) <- 'bbox'
  sf_bbox.ak2 <- st_as_sfc(bbox.ak2) |>
    st_set_crs(st_crs(sf_wgs84))
  
  sf_wgs84.ak1 <- sf_wgs84 |>
    st_intersection(sf_bbox.ak1)
  
  sf_wgs84.ak2 <- sf_wgs84 |>
    st_intersection(sf_bbox.ak2)
  
  sf_wgs84.ak <- rbind(sf_wgs84.ak1, sf_wgs84.ak2)
  
  sf_albersUsa.ak <- sf_wgs84.ak |>
    st_transform(3338)
  
  st_crs(sf_albersUsa.ak) <- st_crs(3857)
  
  st_geometry(sf_albersUsa.ak) <- st_geometry(sf_albersUsa.ak) * 0.35 + c(-1950000, 100000)
  
  st_crs(sf_albersUsa.ak) <- st_crs(3857)
  
  
  # select features in Hawaii area and transform
  bbox.hi <- c(xmin = -161, ymin = 18, xmax = -154.1, ymax = 22.7)
  class(bbox.hi) <- 'bbox'
  sf_bbox.hi <- st_as_sfc(bbox.hi) |>
    st_set_crs(st_crs(sf_wgs84))
  
  sf_wgs84.hi <- sf_wgs84 |>
    st_intersection(sf_bbox.hi)
  
  sf_albersUsa.hi <- sf_wgs84.hi |>
    st_transform('ESRI:102007')
  
  st_crs(sf_albersUsa.hi) <- st_crs(3857)
  
  st_geometry(sf_albersUsa.hi) <- st_geometry(sf_albersUsa.hi) + c(-1000000, -370000)
  
  st_crs(sf_albersUsa.hi) <- st_crs(3857)
  
  
  # select features in CONUS and transform
  bbox.conus <- c(xmin = -133, ymin = 21.5, xmax = -61, ymax = 51.5)
  class(bbox.conus) <- 'bbox'
  sf_bbox.conus <- st_as_sfc(bbox.conus) |>
    st_set_crs(st_crs(sf_wgs84))
  
  sf_wgs84.conus <- sf_wgs84 |>
    st_intersection(sf_bbox.conus)
  
  sf_albersUsa.conus <- sf_wgs84.conus |>
    st_transform(5070)
  
  st_crs(sf_albersUsa.conus) <- st_crs(3857)
  
  sf_albersUsa <- sf_albersUsa.conus |>
    rbind(sf_albersUsa.ak) |>
    rbind(sf_albersUsa.hi)
  
  plot(sf_albersUsa, max.plot = 1)
  
  st_write(sf_albersUsa, outfile)
}