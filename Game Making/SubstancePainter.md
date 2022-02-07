# Substance Painter cheatsheet :

[Tutorial](https://www.youtube.com/playlist?list=PLB0wXHrWAmCwnqWfKdGEmbtSKN2EzvLrY)

## Shortcuts

### Camera
* Rotate / Move / Zoom: `Alt + Left/Mid/Right Mouse`
* Snap Rotate: `Alt + LMB`
* Rotate scene lighting: `Shift + Right Mouse Drag`

### Material
* `Ctrl + drag` a material onto a model to assign it to an ID and automatically create a layer

### Painting
* Brush size: `Ctrl + RMB + drag`
* Brush angle: `Ctrl + LMB + drag`

## ID Map
* Add vertex color in Blender to use it as an ID Map.
* In Substance: Texture Set Settings > Bake Mesh Map > ID: set Color Source = Vertex Color > Bake
* Add Black Mask > Add Color Selection Effect > Pick Color

## [Import in Unreal](https://sbcomputerentertainment.com/other-2/editor/how-to-import-substance-painter-textures-into-ue4/)
1. Uncheck the `sRGB` on the OcclusionRoughnessMetallic texture
2. Set the normal map to "NormalMap"
3. Link the RGB from OcclusionRoughnessMetallic respectively to: AO, Roughness, Metallic

## Misc
- [Substance Designer](https://www.artstation.com/marketplace/p/dNBVB/substance-designer-survival-kit-part-1