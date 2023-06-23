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


# Geopandas spatial join (need one point data, and the other with polygon data)
# Since point is included in the polygon, it will have an intersection and eventually inner join becomes possible.

new_gdf1 = gpd.sjoin(gdf_shp_poly, gdf_geo_pnu, how = "inner", op = "intersects") -> this one worked!

join_left_df = pointdf.sjoin(polydf, how="left")

join_right_df = pointdf.sjoin(polydf, how="right")

pointdf.sjoin(polydf, how="left", predicate="within")

pointdf.sjoin_nearest(polydf, how="left", distance_col="Distances")

# 
```

```
# Converting Pandas dataframe latitude & longitude to geopandas point 
df_sejong['geometry'] = df_sejong.apply(lambda x: Point((float(x.lng), float(x.lat))), axis=1)
df_sejong

gdf = gpd.GeoDataFrame(df_sejong, geometry='geometry')
gdf

gdf = gdf.set_crs("epsg:4326")
gdf.to_file('sejong.shp', driver='ESRI Shapefile', encoding = "cp949")
```
```
# Converting pandas x,y to geopandas x,y and saving it as geopandas dataframe
gdf = geopandas.GeoDataFrame(
    df, geometry=geopandas.points_from_xy(df.Longitude, df.Latitude))
```    
```
# Convert dataframe with geo information to a geodataframe and save it into geopackage file
gdf2 = gpd.GeoDataFrame(df2, geometry='geometry')
gdf2.to_file("test.gpkg", driver = "GPKG", encoding = "cp949")
```    
```
# Extract point coordinates from polygon
gdf_iksan['center_point'] = gdf_iksan.centroid
```
```
# Convert EPSG:5186 to EPSG:4326
# First, set original geodataframe's crs based on the coordinates
gdf_panel = gpd.GeoDataFrame(df_nongji, geometry = gpd.points_from_xy(df_nongji['x'], df_nongji['y']), crs = 'EPSG:5186')
# or
gdf_panel = gdf_panel.set_crs("epsg:5186")
# and convert it to desired crs using to_crs
gdf_panel = gdf_panel.to_crs('epsg:4326')
```    
