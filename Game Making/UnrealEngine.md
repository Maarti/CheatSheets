# Unreal Engine cheatsheet

[UE style guide](https://github.com/Allar/ue5-style-guide)

## Static Mesh
 - Use centimeters as unit in DCC (= Digital Content Creation, like Blender)
 - Place pivot point at world origin (0,0,0) in DCC
 - Each material requires the model go through another rendering pass
 - Relocate pivot point (temporarily): `Middle mouse + drag` the sphere on the gizmo
 - Collision:
   - Save simple collision along with the object in DCC with the name: `UCX_[object_name]_01` (or any number suffix)
   - Duplicate a collider: `Alt + drag` to duplicate
 - Use Unreal LOD generation (use LOD coloration mode in editor)

## Animations
Open Skeletal Mesh => Animation => Move bone => click (+) to add keyframe

## [Lighting](https://docs.unrealengine.com/4.26/en-US/BuildingWorlds/LightingAndShadows/)
 - If we have overlapping texture UV (multiple parts of mesh using same part of the texture), we can let Unreal auto-generate the lightmap so the lighting won't be the same on the overlapping parts. 
 - Don't overlap more than 3 stationary lights (exponential cost) (-> the 4th will be marked with a red cross)
 - Screenspace reflection = reflection of objects currently visible on screen (you won't see the reflection as soon as the object is no longer visible)
 - Lightmass settings for architectural visualization:
   - Static Lighting Level Scale: 1.0 *(lightmass detail)*
   - Num Indirect/Sky Bounces: 3~10 *(scene brightness)*
   - Indirect Lighting Quality: 1~4 *(increases final gather ray count, reducing artifacts)*
   - Indirect Lighting Smoothness: 1~1.3 *(blurs indirect light results, reducing noise)*
   - Compress Lightmaps: Disabled *(improves quality, but increases lightmap size by a factor of 4)*
 - LightMassImportanceVolume: Restrict GI to this area (outside will only get low-quality GI)
 - [World Outliner] Circle near object:
   - Orange: Movable
   - Yellow: Stationnary
   - None: Static
 
## Material
 - Create "constant 3" node (for RGB color): `hold 3 + click`

