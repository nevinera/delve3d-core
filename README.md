# delve3d-core

The core world for [delve3d](https://github.com/nevinera/delve3d).

## Layout

```
world.json                     name, format version, level cap, starting gear and locations,
                               continents, dungeons, world connections, day/night timing
places/
  biomes/
  continents/<continent>/
    index.json                 each tile coordinate's zone and which layers it has
    zones/<zone>.json          sketch, metadata (name, level range, music), tile list, subzones
    tiles/surface/12/-4.dlt.gz sharded by x
    tiles/-1/12/-4.dlt.gz
  dungeons/<dungeon>/
    dungeon.json               group size, entrance/arrival, sketch, subzones, encounter order
    index.json
    tiles/surface/0/0.dlt.gz
    encounters/<boss>.json     boss unit types, adds, phases, scripted abilities, loot table
models/
  kits/<culture>/              structures and props, grouped by culture
  bodies/  palettes/
unit_types/  classes/  items/  quests/
```

- Tiles are filed by continent coordinate. Zones and subzones are metadata, so moving a zone
  border never moves a file.
- Each object is its own file. The bundler writes a `_bundle.json` per folder, and CI fails when
  one is stale. The game fetches bundles, and streams tiles one at a time through `index.json`.
- Abilities live inside the unit types and classes that use them.
- This world carries its own kits and biomes. To reuse one from another world, copy it.
