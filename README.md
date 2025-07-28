# A Scalability Mod for [WUCHANG: Fallen Feathers](https://store.steampowered.com/app/2277560/WUCHANG_Fallen_Feathers/)

First off all, as of patch 1.3, this game has decided that Native (100%) resolution is **dead**. Despite having an in-game slider for the resolution scale, it still uses specific resolution targets, so the slider might as well be a drop-down instead.

| Scale | Actual Value |
| -- | -- |
| 100% | 2560x1440, 100% of 1440p, Native (non-existent) |
|67% - 100% | 1716x965, 67% of 1440p, Quality |
|59% - 66% | 1485x836, 58% of 1440p, Balanced |
|31% - 58% | 1280x720, 50% of 1440p, Performance |
|25% - 30% | 853x480, 33% of 1440p, Extreme Performance |

Other than that, the game exhibits some annoying pop-in issues with some objects (like hanging cloth or some leaves on the ground) even at max settings. This mod seeks to improve upon these minor gripes, with more or less the same performance.

> Every single setting was tweaked with **NATIVE** resolution and **TAA OFF** in mind, therefore making sure that noise, flickering, and jitter is minimized as much as possible.

# Anti-Aliasing Quality
AA can now be completely turned off. Contact shadows are toggled off when TAA is off as it causes obscene amounts of flickering and noise. It is passable with TAA on. Optimized with [Hybred's Best Unreal Engine Anti-Aliasing Tweaks](https://www.reddit.com/r/MotionClarity/comments/1gghasv/best_unreal_engine_antialiasing_tweaks/).

Low - AA Off  
Mid - TAA  
High - TSR  

# Post-Processing
Motion blur actually looks good now, if you want to use it for some reason.

Low - Bloom is complete disabled.  
Mid - Minor DOF/Bloom/AO changes.  
High - Full Resolution Bloom, higher quality Lens Flare and DOF.

# Shadow Quality
This game utilizes UE5's Virtual Shadow maps so heavily that it looks outright broken with it disabled. I've tried my best to make it look as clean as possible.

I've decided to move the `r.Shadow.Virtual.MaxPhysicalPages` setting to Texture Quality. Too small of a value can cause shadows to flicker, pixelate, or outright disappear. Quite VRAM intensive.

Oh, and it also changes some light source's draw distance.

Low - Disables jitter at the cost of no shadow filtering (very sharp shadows with no penumbra simulation).  
Mid - Minimized jitter and minimal shadow filtering.  
High - Minimized jittering, otherwise same as vanilla.  
Ultra - Very slightly higher quality shadows with minimal jittering.  
Extreme - Doubled light source draw distance (see candles).  

# Effects Quality
Moved the SSR values to be controlled by the dedicated Reflection Quality setting. Subsurface Scattering set to auto across the board (couldn't see a visual difference).

# Viewing Distance
Minor changes. 

Low - More pop-in, NPC shadows are culled.  
Mid - Unchanged from stock.  
High - Pushed draw distance even more.  

# Texture Quality
This mainly adjusts the VRAM limits and anisotropic filtering. Now it also adjusts Virtual Shadow map VRAM cost. These values are unchanged from stock.

| Setting | Anisotropic Filtering | Texture Buffer Size | VSM Physical Pages |
| -- | -- | -- | -- |
| Low | OFF | 2000 MB | 1024 MB |
| Mid | x8 | 2000 MB | 2048 MB |
| High | x16 | 6144 MB | 5500 MB |

# Vegetation Quality
Set `foliage.MinimumScreenSize` to 0 across the board. This fixes the horrendous pop-in of some objects like the hanging cloths and whatnot.

Low - Normal foliage draw distance.  
Mid - Doubled foliage draw distance. Faster by about ~2fps due to an unused lower material quality level (3).  
High - Quadrupled foliage draw distance.  

# Volumetric Fog
Minor adjustments.

Low - More pixelated fog.  
Mid - Lowered quality from vanilla.  
High - Higher quality from vanilla.

# Global Illumination
The game looks significantly different with Lumen turned off. I have tried to minimize the boiling and flicker as much as possible, but higher settings really tank framerate.

Off - Disabled Lumen.  
Low - Basic lumen with disabled bounce lighting.  
Mid - Full lumen with some noise and jitter.  
High - More objects are traced, minimized jitter at the cost of obscene amounts FPS.  

## Ambient Occlusion (Unchanged)
This setting weirdly doesn't respect the preset changes. This simply toggles between using ScreenSpaceBentNormal or DiffuseIndirectSSAO, both Lumen functions, mutually exclusive from each other. 

# Reflection Quality
Moved `r.AOGlobalDistanceField` to the Global Illumination setting. This enables bounce lighting and a higher quality version of Lumen's SSR with less occlusion artifacts. This setting now correctly adjusts how reflections look, whether lumen is on or not.

Low - Disables SSR and Lumen completely.  
Mid - Half resolution SSR. Reduced lumen reflections.  
High - Full resolution SSR. Full lumen reflections.  
