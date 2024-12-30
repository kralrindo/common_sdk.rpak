**SDK RPAKs for R5Reloaded Modded Apex Project**  
Created by: @KralRindo  
  
**Credits**  
Repak, 010 Respawn Templates, RSX, and Model Converter: rexx, IcePixelx, Rika, AmosModz  
  
**Required Tools**  
[Repak](https://github.com/r-ex/RePak)  
[Respawn-mdl Templates](https://github.com/IJARika/respawn-mdl)  
[010 Editor](https://www.sweetscape.com/010editor/)  
[RSX](https://github.com/r-ex/rsx)  
  
R5Reloaded supports asset types from Season 0-5.  
  
**Asset Types**  
  
dtbl: Datatables, Comma-separated values (CSV). Custom or manually ported from Apex Seasons.  
shds: Material shadersets, Multi Shader Wrapper (MSW). Connects two different shaders into one set. Only supported by the latest RSX version.  
txtr: Texture assets, DirectDraw Surface Images (DDS). Ensure you check the texture types in the txtr section.  
matl: Materials, JavaScript Object Notation File (JSON). Exported with RSX or custom-made. Contains all material data.  
aseq: Animation sequences, Respawn Sequences (RSEQ). Animation data for Respawn Models, Can’t be custom-made, needs to be exported using RSX.  
arig: Animation rigs. Respawn Rigger Design File (RRIG). Model rig for Respawn Models, Can’t be custom-made, needs to be exported using RSX.  
rmdl: Models, Respawn Model (RMDL)  
uimg: Atlas, This is used for ui images, minimaps and loadscreens. See atlas section.  
  
**Asset Order in Main RPak JSON**  
txan > dtbl > shdr > txtr > matl > aseq > arig > rmdl > uimg  
  
## TXAN Assets  
Txan is required for animated ptcu/ptcs materials, it controls the texture arrays and material animations.
  
```json
{
    "_type": "txan", 
    "_path": "texture_anim/(txan path).rpak"  //TXAN file path
}
``` 
## DTBL Assets  
This asset type is used to define CSV format data tables within the RPak. Data tables can be used to configure and store structured data like weapon stats, loot tables, or other game-related information. Can be referenced within the scripts to manage various gameplay elements.  
  
We recommend structuring your CSV files with proper headers to ensure they are interpreted correctly by the game. A broken datatable can cause crashes.  
  
```json
{
    "_type": "dtbl",  //Asset Type, in this case dtbl (datatable)
    "_path": "datatable/(datatable path).rpak"  //CSV file path
}
```
  
## SHDS Assets  
ShaderSets are used to define the set of shaders for materials, which control how objects are rendered, including effects like lighting, shadowing, and texture mapping. These assets must be exported with the RSX tool and are stored with the .msw extension.  
  
```json
{
    "_type": "shds",  //Asset Type, in this case, 'shds' for ShaderSet
    "_path": "shaderset/uberTnBnInterpAoCavOpmCbstCutVbweR5AoAnisoDirAmtUv0m0PSSamp222222222_sknp.rpak"  //Path to the ShaderSet .msw file
}
```
  
Key Fields:  
_type: This specifies the asset type. For ShaderSets.  
_path: The file path to the ShaderSet asset (e.g., "shaderset/uberTnBnInterpAoCavOpmCbstCutVbweR5AoAnisoDirAmtUv0m0PSSamp222222222_sknp.rpak"). This path points to the .msw file that contains the compiled ShaderSet, which is used by materials in the game.  
  
Additional Considerations:  
Exporting with RSX: ShaderSets need to be exported using the RSX tool to ensure that the .msw file is correctly compiled.  
If the ShaderSet doesn't already exist in the R5Reloaded build, it needs to be explicitly referenced and included in the main RPak JSON.  
  
## TXTR Assets  
This asset type is being used to add .dds type textures into the rpak, it's not being required to add if texture path is correct in the material json.  
  
We strongly recommend using mipmapped textures for better performance and better look.  
  
```json
{
    "_type": "txtr", //Asset Type, in this case txtr which is texture
    "_path": "texture/(texture path).rpak"  //DDS file path
}
```
  
Required .DDS Types:  
  
_col (albedo): BC7 sRGB  
_nml (normal): BC5U / R8G8  
_gls (gloss): BC4U  
_spc (specular): BC7 sRGB  
_ilm (emissive): BC7 sRGB  
_ao (ambient occlusion): BC4U  
_cav (cavity): BC4U  
_opa (opacity): BC4U  
  
UI Assets:  
BC7 sRGB  
  
Loadscreens:  
BC1 sRGB (Low Quality)  
BC7 sRGB  
  
Minimap:  
BC1 sRGB  
  
## MATL Assets  
Material assets (matl) are a core part of how objects are rendered in the game, as they define properties like shaders, textures, blend states, and surface properties. Materials are packaged in .rpak files but internally reference a JSON file that holds the actual material data.  
  
Overview of MATL Assets:  
Material JSON: The material data contains information about the shader used, textures applied, blend states, depth/stencil settings, surface properties, and more.  
Reference in Main RPak JSON: MATL asset refers to the material file by pointing to an .rpak file, which is responsible for loading the material data JSON.  
Ported Materials: If a material was ported from another Apex build, or if it uses special materials like depth or colpass materials, these must be explicitly included in the RPak.  
  
This is an example of how a material asset is referenced in the main RPak JSON.  
  
```json
{
    "_type": "matl",  //Asset Type (Material)
    "_path": "material/models/Weapons_R2/epg/epg_mag_sknp.rpak"  //Path to the material .rpak file
}
```
  
The "_type": "matl",  
The "_path" "material/jsonpath.rpak" specifies the path to the .json file that contains the material data.  
  
Material Data JSON Example:  
This is an example of the material data JSON that would be loaded when the material .json file is referenced. It contains the properties of the material, including its textures, shader, blend states, and other properties.  
  
```json
{
	"name": "models/Weapons_R2/epg/epg_mag",
	"width": 512,
	"height": 512,
	"depth": 0,
	"glueFlags": "0x56000122",
	"glueFlags2": "0x100000",
	"blendStates": [
		"0xF0138286",
		"0xF0138286",
		"0xF0008286",
		"0x0",
		"0xF0138286",
		"0x0",
		"0x80500002",
		"0x0"
	],
	"blendStateMask": "0x5",
	"depthStencilFlags": "0x7",
	"rasterizerFlags": "0x6",
	"uberBufferFlags": "0x0",
	"features": "0x1F5A92BD",
	"samplers": "0x1D0300",
	"surfaceProp": "plastic",
	"surfaceProp2": "",
	"shaderType": "sknp",
	"shaderSet": "0x15797A5751148156",
	"$textures": {
		"0": "texture/models/Weapons_R2/epg/epg_mag_albedoTexture.rpak",
		"1": "texture/models/Weapons_R2/epg/epg_mag_normalTexture.rpak",
		"2": "texture/models/Weapons_R2/epg/epg_mag_glossTexture.rpak",
		"3": "texture/models/Weapons_R2/epg/epg_mag_specTexture.rpak",
		"5": "texture/models/Weapons_R2/epg/epg_mag_aoTexture.rpak",
		"6": "texture/models/Weapons_R2/epg/epg_mag_cavityTexture.rpak",
		"7": "texture/models/Weapons_R2/epg/epg_mag_opacityMultiplyTexture.rpak"
	},
	"$depthShadowMaterial": "0x0",
	"$depthPrepassMaterial": "0x0",
	"$depthVSMMaterial": "0x0",
	"$depthShadowTightMaterial": "0x0",
	"$colpassMaterial": "0x0"
}
```
  
Key Fields in Material Data JSON:  
  
name: The name of the material (used for reference).  
width and height: Texture dimensions (used for material setup).  
glueFlags and glueFlags2: Various flags related to material behavior.  
blendStates: Blend states that define how materials blend with others.  
depthStencilFlags, rasterizerFlags, uberBufferFlags: Various rendering flags.  
features: Additional features or settings that modify how the material behaves.  
samplers: Defines how textures are sampled by the GPU.  
surfaceProp: Defines the surface property (e.g., plastic).  
shaderType: The shader type used (in this case, sknp).  
shaderSet: A reference to the ShaderSet associated with this material.  
$textures: A dictionary of textures applied to the material, where keys represent the texture slots (e.g., albedo, normal, spec, etc.) and the values are paths to the texture .rpak files.  
$depthShadowMaterial, $depthPrepassMaterial, etc.: Optional fields that point to specific depth or colpass materials. These should be included if the material uses them.  
  
If the material uses special depth or colpass materials ($depthShadowMaterial, $depthPrepassMaterial, etc.), these materials must also be ported and included in the RPak. These materials are used in advanced rendering techniques like shadow mapping or post-processing effects.  
  
Custom materials may require special handling for compatibility. Check below for the texture slot types.  
  
slot0: _col  
slot1: _nml  
slot2: _gls/_exp  
slot3: _spc  
slot4: _ilm  
slot5: _ao  
slot6: _cav/cvt  
slot7: _opa  
slot8: detail/camo  
slot9: _dm_nml/_nml (detail normal map)  
slot10: _msk (detail texture mask)  
Blend Materials (used for maps):  
slot16: _bm (blendmap)  
slot22: _col  
slot23: _nml  
slot24: _gls/_exp  
slot25: _spc  


## RRIG Assets (Animation Rigs)  
Animation Rigs (rrig) define how models animate by specifying the bone structure and animation layers. These rigs are used by .rmdl models to apply various animations, such as walking, running, aiming, etc. When an animation seq is referenced in a rig, the associated animation sequences are automatically loaded by the RPak, so you don't need to explicitly reference them separately.  
  
These assets define the skeleton and animation layers for a model. Each animation rig can have multiple animation sequences that are applied to a model based on the rig's bone structure.  
Sequences: Animation sequences are included by the RPak tool when the animation rig is loaded. They don't need to be explicitly listed unless additional customization is needed.  
  
This is an example of how an animation rig (.rrig) is referenced in the main RPak JSON file. It also includes a list of animation sequences that belong to this rig.  
  
```json
{
    "_type": "arig",  //Asset Type (Animation Rig)
    "_path": "animrig/robots/drone_air_attack/drone_air_attack_plasma.rrig", //Path to the animation rig file
    "$sequences": [
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/aim_layer.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/aim_run.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/aim_walk.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/alert.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/attack.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/idle.rseq",
        "animseq/robots/drone_air_attack/drone_air_attack_plasma/reload.rseq"
    ]
}
```
  
Key Fields in RRIG Asset JSON:  
  
_type: "arig" specifies that this is an animation rig asset.  
_path: "animrig/filepath.rrig" The path to the .rrig file that defines the animation rig.  
$sequences: A list of animation sequences associated with the rig. These are applied based on the animation rig's configuration, so they are automatically loaded by the RPak tool.  
  
Bone Structure: The .rrig file defines the skeleton, so it must be compatible with the model (.rmdl) that references it. This ensures the animations are applied correctly to the model's bones.  
Sequences and Animations: If the animation sequences (e.g., idle, attack) have been defined in the rig, they are automatically linked to the model. However, any additional animation sequence that isn't part of the original rig cannot be added into the rig. Otherwise this will cause a crash.  
  
## RSEQ Assets  
Animation Sequences (rseq) are animation files that define the movement or behavior of a model, such as idle animations, attack animations, etc. These sequences are often associated with Animation Rigs (.rrig) and Models (.rmdl). However, if they are not part of a rig or model, they must be explicitly included in the main RPak JSON.  
  
It is essential to not rename the .rseq files. Renaming these files will cause a breakage in the GUIDs (Global Unique Identifiers) of the animations, resulting in missing references and crashes.  
  
```json
{
    "_type": "rseq",  //Asset Type, in this case 'rseq' for animation sequences
    "_path": "animseq/props/testanimfolder/close_idle.rseq"  //Path to the animation sequence file
}
```
  
  
In most cases we don't need this asset type, only use for this would be replacing an animation sequence from R5Reloaded build.  
  
## MDL_ Assets  
This asset type is used to define 3D models (RMDL) within the RPak. These models can be static or dynamic, and they may include animations and physics files. Models are typically loaded into the game by their file paths and can be used as props, characters, or other interactive elements.  
  
```json
{
    "_type": "mdl_",  //Asset Type, in this case mdl_ (model)
    "_path": "mdl/props/kralstest/thisisa_testprop.rmdl",  //Path to the model file
    "$animrigs": [  //Optional: Path to animation rigs for this model
        "animrig/props/prowler_hatch_tt/prowler_hatch_tt.rrig"
    ],
    "$sequences": [  //Optional: Animation sequences for the model
        "animseq/props/prowler_hatch_tt/close.rseq",
        "animseq/props/prowler_hatch_tt/close_idle.rseq",
        "animseq/props/prowler_hatch_tt/open.rseq",
        "animseq/props/prowler_hatch_tt/open_idle.rseq",
        "animseq/props/prowler_hatch_tt/prowler_hatch_tt/prop_bloodhoundTT_hatch_spawn.rseq"
    ]
}
```
  
Key Fields:  
  
_type: Asset type, always set to "mdl_" for model assets.  
_path: Path to the model file within the game assets (e.g., mdl/props/kralstest/thisisa_testprop.rmdl).  
$animrigs: An array of paths to the animation rigs associated with the model. These rigs define how the model will animate (e.g., animrig/props/prowler_hatch_tt/prowler_hatch_tt.rrig).  
$sequences: Optional array of paths to animation sequences for the model. If a model doesn’t have an animation rig but still requires animations, these sequences can be applied directly to the model. Sequences included within the model doesn't require to be added seperately aka RePak will auto add them.  
  
Important Notes:  
Materials: Every material used by the model must be included in the main rpak json. Missing materials may result in GUID errors.  
Physics Files: If the model is interactive or needs physics behavior, make sure to include the associated .phy file.  
  
  
//=========================================================  
//					  Surface Types    				     //  
//=========================================================  
  
// -----------------------------  
// Surface Materials  
// -----------------------------  
  
default
metal_titan
solidmetal / NOTE: Almost nothing is solid metal - so "metal" is sheet metal
metal / NOTE: Only flag a few things as "solidmetal" (I-Beams, anvils, etc)
metal_box / Smaller metal box (< 2' width/height/depth)
metalpanel / Thick solid steel panel - used for solid wall, floor, machine construction
metalgrate
metalvent
dirt
tile
xo_shield
wood / NOTE: materials should use wood_box, wood_crate, wood_plank, wood_panel etc
wood_solid
water
concrete
glass
glass_breakable
flesh
armorflesh / NOTE: Flesh for physics, metal for bullet fx
sand
mud
grass
brokenglass
gravel
bloodyflesh
  
// -----------------------------  
// Non Surface Materials  
// -----------------------------  
  
shellcasing_small
shellcasing_large
weapon / NOTE: Weapon models - sounds for when weapons drop
computer
canister / NOTE: Large oxygen tank, propane tank, welding tank
metal_barrel / NOTE: Larger metal barrel, metal oil drum
glassbottle / NOTE: Glass soda bottle, cup, plate, jar
pottery / NOTE: Ceramic jug, mug
grenade / NOTE: Solid hand grenade
grenade_triple_threat
bouncygrenade
  
// -----------------------------  
// world materials  
// -----------------------------  
  
metal_bouncy
slipperymetal / Note: Airboat pontoons have very low friction
slipperyslime
wood_lowdensity
wood_box / Note: Small crate
wood_crate / Note: Large crate, large wood furniture (bookcases, tables)
wood_plank / Note: wood board, floorboard, plank
wood_furniture / Note: small wood furniture - chairs, small tables
wood_panel / Note: wood panel - plywood panel, wood door panel
slime
quicksand
rock / Note: Solid rock (small sounds)
lava_rock
lava_rock_hot / Note: Lava rock that shows a glows when shot
lava_flow / Note: scrolling uv lava, like water.
porcelain / Note: tubs, urinals, sinks
boulder / Note: Large solid rock (large sounds)
asphalt
brick
concrete_block / Note: 9x12 prefabricated concrete cinder blocks
chainlink / Note: chainlink fencing material
chain / Note: metal chain
alienflesh
watermelon
snow
ice
carpet
plaster / Note: drywall, office wall material, sheetrock
cardboard / Note: carboard box
plastic_barrel / Note: larger plastic barrel, hollow, soft plastic
plastic_box / Note: small - medium plastic box, hard plastic
plastic / Note: smaller generic hard plastic
item / Note: small med kit, smaller tech items, battery
floatingstandable
rubber
rubbertire
jeeptire
slidingrubbertire
brakingrubbertire
slidingrubbertire_front
slidingrubbertire_rear

  
// -----------------------------  
// objects  
// -----------------------------  
  
floating_metal_barrel
plastic_barrel_buoyant
roller
popcan
paintcan
paper
papercup
ceiling_tile
default_silent
player
player_control_clip
foliage
Underground_Cube
Turret_Gib
metal_spectre
arc_grenade
upholstery
flyerflesh
ammo_box
Helmet
Large_Backpack
Small_Backpack
Large_Medkit
Small_Medkit
Att_Scope
Att_Sup
Wpn_AR
Wpn_Snipe
Wpn_SMG
Wpn_Pistol
Wpn_Shotgun
Vest
Mags
Cyn_Medkit
Frag
ArcBlade
BatteryShield
reflective
WeightedCube_Bounce
PaintBomb
sphere2
