# libgdx-tiledmappacker
A standalone version of gdx-tools' TiledMapPacker.

See the Releases section for runnable JARs.

[See the libGDX wiki for maybe more information](https://libgdx.com/wiki/tools/texture-packer), but that probably isn't
the right article. The Tiled Map Packer wasn't really documented like the other tools in libGDX.

Given one or more TMX tilemaps, packs all tileset resources used across the maps, or the resources used per map, into a
single, or multiple (one per map), `TextureAtlas` and produces a new TMX file to be loaded with an `AtlasTiledMapLoader`
loader. Optionally, it can keep track of unused tiles and omit them from the generated atlas, reducing the resource size.

**Usage (all desktop platforms)**:

`java -jar TiledMapPacker-1.11.0.1.jar inputDir [outputDir] [--strip-unused] [--combine-tilesets] [-v]`

The inputDir should contain a .tmx file and any tilesets it uses, placed how the .tmx map specifies them. The outputDir,
if not specified, will be the folder `output/` next to the inputDir. If `--strip-unused` is present, then tiles that
aren't in the .tmx map will not be present in the resulting atlas. if `--combine-tilesets` is present, all tilesets will
be merged into "some kind of monster" tileset; this is not currently recommended unless you know what you are doing. If
`-v` is present, this uses verbose mode, and will print much more output about everything it does.

The original TMX map file will be parsed by using the `TmxMapLoader` loader, thus access to a valid OpenGL context is
**required**; that's why an `Lwjgl3Application` is created by this preprocessor (with a tiny window).

The new TMX map file will contain a new property, "atlas", whose value will enable the `AtlasTiledMapLoader` to
correctly read the associated `TextureAtlas` representing the tileset.

This was taken from inside [libGDX](https://github.com/libgdx/libgdx) and moved so it can be run more easily from
outside that framework. It still has the same license as libGDX.

# Changelog

1.11.0.1 : Small release to minimize the JAR with ProGuard and to use `gdx-lwjgl3-glfw-awt-macos` to make running this
easier on MacOS.

1.11.0.0 : Initial release; this included the port to use PixmapPacker and LWJGL3 instead of TexturePacker and LWJGL2.
