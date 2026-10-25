# delve3d-core

The core world for [delve3d](https://github.com/nevinera/delve3d).

## Layout

```
world.json
kits/  biomes/
continents/<continent>/
  index.json                   each tile coordinate's zone and which layers it has
  zones/<zone>.json            sketch, metadata (name, level range, music), tile list, subzones
  tiles/surface/12/-4.dlt      sharded by x
  tiles/-1/12/-4.dlt
dungeons/<dungeon>/            each its own small grid, same shape
```

Tiles are filed by continent coordinate. Zones and subzones are metadata, so moving a zone
border never moves a file.
