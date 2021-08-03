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
 - Don't overlap more than 3 stationary lights (exponential cost) (-> the 4th will be marked with a red cross) (check it with "Light complexity" mode)
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
   
 Rotating light direction with the mouse: select the directional light (that is "Atmoshpere Sun Light"), hold `Ctrl+L` and move mouse
 
## Material
 - Create "constant 3" node (for RGB color): `hold 3 + click`
 - Use a "static switch" node for functionnalities that are not useful all the time (eg. using BaseColor or BaseTexture)

## Landscape
 - Use [World Machine](https://www.world-machine.com/) to simulte/generate a terrain height map
 - Hold `Shift` to reverse the current brush
 - [Add grass proceduraly](https://learn.unrealengine.com/course/3590620/module/6960224) with Landscape Grass Type

## Sequencer
 - Follow current camera in viewport: click the camera icon in master sequence "Lock viewport to shot"

## Optimization
 - Always have texture size that are power of 2 in order for mipmap to works (else, the texture will always take its full size in memory even if its far away from the camera)
 - Use RGB channels instead of multiple image
 - Disable `sRGB` on masks and normal maps
 - If 90% of your object are not transparent, don't use a single Parent Material for all your game because the cost of translucency will be applied to all objects
 - Use a "Cull Distance Volume": make objects of a given size disapear if they are at a given distance of the camera (you can also use Max Draw Distance on actors)
 - Use "[Merge Actors](https://docs.unrealengine.com/4.26/en-US/Basics/Actors/Merging/)" to merge multiple static meshes and materials into one (doesn't work well with tiled textures)
 - [Hierarchy LOD](https://docs.unrealengine.com/4.26/en-US/BuildingWorlds/HLOD/): replaces multiple static meshes with a single one at long view distances
 
## Miscellaneous
 - Type `help` in the console to generate an interactive help in the web browser