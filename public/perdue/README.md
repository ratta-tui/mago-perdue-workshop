
## Hamilton County

### 1. Terrain

```sh
docker run --rm -v "YOUR_PROJECT_DIR\perdue:/workspace" gaia3d/mago-3d-terrainer  --input /workspace/org/dem/ --output /workspace/output/terrain/ --log /workspace/output/terrain/log.txt -cn --minDepth 0 --maxDepth 17 `
```

### 2. Buildings

```sh
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" gaia3d/mago-3d-tiler --input "/workspace/org/buildings/Building_foot_prints_meter_clip.geojson" --output "/workspace/output/tileset/buildings/"  --inputType geojson --crs 4326 --heightColumn "rel_height_2_meter" --terrain "/workspace/org/dem/hamilton_dem_navd88_meters_4326_clip.tif" --log "/workspace/output/tileset/buildings/log.txt" `
```


### 3. Point Cloud

```sh
 docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" gaia3d/mago-3d-tiler --input "/workspace/org/pointcloud/forest_meter_4326.laz" --output "/workspace/output/tileset/pointcloud" --log "/workspace/output/tileset/pointcloud/log.txt" -inputType "laz" --crs 4326 --pointRatio 70 --tilesVersion 1.0 `
```


### 4. trees(i3dm)

```shell
docker run --rm -v "YOUR_PROJECT_DIR\public\perdue:/workspace" gaia3d/mago-3d-tiler --scaleColumn "rel_height_m" -inputType gpkg --input "/workspace/org/forest/forest_meter_clip.gpkg" -outputType i3dm --output "/workspace/pre-made-output/tileset/forest" --crs "4326" --instance "/workspace/org/forest/instance-LOD3.glb" --terrain "/workspace/org/dem/hamilton_dem_navd88_meters_4326_clip.tif" --log "/workspace/pre-made-output/tileset/forest/log.txt" --tilesVersion 1.0

```






