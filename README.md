# Geopandas
```
# Reading shp file
gdf = gpd.read_files(s, encoding = "cp949")

# Converting to a different coordinating system
gdf.to_crs('epsg:4326')

# Creating center point and its x,y coordinates separately

gdf['Center_Point'] = gdf.centroid

gdf['x'] = gdf.CP.x
gdf['y'] = gdf.CP.y

# Creating geometry POINTS

gdf = gpd.GeoDataFrame(gdf, geometry = gpd.points_from_xy(gdf['x'], gdf['y']), crs = 'EPSG:4326')


# Geopandas spatial join
join_left_df = pointdf.sjoin(polydf, how="left")

join_right_df = pointdf.sjoin(polydf, how="right")

pointdf.sjoin(polydf, how="left", predicate="within")

pointdf.sjoin_nearest(polydf, how="left", distance_col="Distances")

```


