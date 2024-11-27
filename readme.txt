Asset RPAKs for R5Reloaded Modded Apex Project.
Assets not included in this repo for keeping everything minimal, required assets can be exported with RSX

Made by @KralRindo

Other credits:

Repak, 010 Respawn Templates, Legion, RSX and Model Converter: rexx#1287, IcePixelx#4931, Rika#1525

How to use REPak to make custom asset rpaks for R5Reloaded. Note: This part is for how to port Season 4-6 Apex assets, not for custom models

Required Tools
Repak: https://github.com/r-ex/RePak
Respawn-mdl Templates: https://github.com/IJARika/respawn-mdl
010 Editor: https://www.sweetscape.com/010editor/
LegionPlus: https://github.com/r-ex/LegionPlus
RSX: https://github.com/r-ex/rsx

R5Reloaded supports season 2.1-5 (Season 6 has collision changes on rmdl) all asset types. For models they need to be exported with legion/RSX as RMDL format.

dtbl: Datatables, Possible to export from legion, edit the way you want and port it to a rpak.
shds/shdr: Export shadersets from rsx.
txtr: Texture assets, required by materials, you don't have to add them if they are included in matl since repak auto adds them.
matl: Materials, legion prints the data it needs in the console, add the flags, shaderset, cpudata and textures.
aseq: Animation sequences, in here it's used for models that doesnt have any animrig but does have animations.
arig: Animation rigs. Animation order needs to be same with what you see in the legion console or RSX json.
rmdl: Respawn's mdl format, you can export and port from s2-s3-s4-s5-s6, or make one yourself with crowbar, blender source tools or export the models as smd with legion and use crowbar to convert them to mdl format. Then rexx's converter does the rest of it.
uimg: This is used for ui images, minimaps and loadscreens, check my jsons to see more details.

Asset order in a json: dtbl > txtr > matl > aseq > arig > rmdl > uimg

Some extra information regarding season 3 apex assets.

//=========================================================
//					Material Slots						 //
//=========================================================

slot1 _col
slot2 _nml 
slot3 _gls/_exp
slot4 _spc
slot5 _ilm
slot6 _ao
slot7 _cav/cvt
slot8 _opa
slot9 detail/camo
slot10 _dm_nml/_nml detail normal map
slot11 _msk detail texture mask
the following are used on blend materials, for maps only. it is a second texture to blend into the main one.
slot17 _bm blendmap
slot23 _col
slot24 _nml 
slot25 _gls/_exp
slot26 _spc


//=========================================================
//					Example material    	    		 //
//=========================================================

    {
      "$type": "matl",  #Asset Type, in this case matl which is material
      "path": "test/test_material",  #Material path, this path is used by world or models
      "type": "wldp",  #Material type, "WLDC, WLDP, WLDU": Used by world materials, "RGDC, RGDP, RGDU": Used by Static Models, "SKNC, SSKNP, SKNU": Used by nonStatic Models,  
      "cpu": "texture/blinn_maya_test/blinn_maya_test",  #CPU Path, required for material to work properly, can be exported using RSX or LegionPlus. It controls characteristic material features like emissive strengt, fade distance etc.
      "blendStates": "F0000000 F0000000 F0000000 F0000000 F0000000 F0000000 F0000000 F0000000",  #Required for BM type materials to work properly
      "samplers": "001D0300",  #Next five entries are flags, controls how material looks (Transparent, wideframe etc).
      "flags2": "56000020",
      "depthStencilFlags": 23,
      "rasterizerFlags": 6,
      "unkFlags": 4,
      "shaderset": "0x000000000000000",  #Shaderset is required for material to render properly, shaderset texture count has to match with Material Textureslotcount or game will likely crash
      "width": 32,  #Material width and weight, same as first slot texture.
      "height": 32,
      "textureSlotCount": 6, #Total texture slots being used by this material, has to match with shaderset.
      "textures": {
        "0": "texture/test/blinn_maya_test_WLDC/blinn_maya_test_albedoTexture",
        "1": "texture/test/blinn_maya_test_WLDC/blinn_maya_test_normalTexture",
        "2": "texture/test/blinn_maya_test_WLDC/blinn_maya_test_glossTexture",
        "3": "texture/test/blinn_maya_test_WLDC/blinn_maya_test_specTexture",
        "5": "texture/test/blinn_maya_test_WLDC/blinn_maya_test_aoTexture"  #Texture entries, textures have to be dds format, check below.
      }
    }

//=========================================================
//					Example Model       	    		 //
//=========================================================

    {
      "$type": "rmdl", #Asset Type, in this case rmdl which is model
      "path": "mdl/props/kralstest/thisisa_testprop.rmdl", #Model path, game calls the models from this path
      "usePhysics": true,  #Define if model has PHY. file
      "static": true,  #Define if model is a static prop, models with only one bone are static props
      "animrigs": ["animrig/props/prowler_hatch_tt/prowler_hatch_tt.rrig" ],  #Animation rig for the model
      "materials": [ "models/vistas/desertlands_mu1/iceland_slopeb_mu1_rgdp" ],  #Material paths, used for replacing the material. Usually isn't needed
      "sequences": [
        "animseq/props/prowler_hatch_tt/close.rseq",
        "animseq/props/prowler_hatch_tt/close_idle.rseq",
        "animseq/props/prowler_hatch_tt/open.rseq",
        "animseq/props/prowler_hatch_tt/open_idle.rseq",
        "animseq/props/prowler_hatch_tt/prowler_hatch_tt/prop_bloodhoundTT_hatch_spawn.rseq"  #Animation sequences, if animations don't have any rig, they can be added to model this way
      ]
    }

//=========================================================
//					Example Datatable      	    		 //
//=========================================================

    {
      "$type": "dtbl",  #Asset Type, in this case dtbl which is datatable
      "path": "datatable/dialogue/blood_tt_dialogue"  #Datatable path, CSV format is being used, datatables doesn't require anything else
    }

//=========================================================
//				 Example Animation Rig      	    	 //
//=========================================================

    {
      "$type": "arig",  #Asset Type, in this case arig which is Animation Rig
      "path": "animrig/props/testrig/animrig.rrig",  #Animation Rig path, this is what models use to locate the rig
        "animseq/props/testanimfolder/close.rseq",
        "animseq/props/testanimfolder/close_idle.rseq",
        "animseq/props/testanimfolder/open.rseq",
        "animseq/props/testanimfolder/open_idle.rseq",
        "animseq/props/testanimfolder/lock.rseq"  #Animation sequences
      ]
    }


//=========================================================
//					Example Sequence      	    		 //
//=========================================================

    {
      "$type": "rseq",  #Asset Type
      "path": "animseq/props/testanimfolder/close_idle.rseq"  #Animation path, these cannot be made customly, can be exported from Apex using RSX and Legion+
    }

//=========================================================
//					Texture Formats 					 //
//=========================================================

_col: BC7 sRGB
_nml: BC5U
_gls: BC4U
_spc: BC7 sRGB
_ilm: BC7 sRGB
_ao:  BC4U
_cav: BC4U
_opa: BC4U

UI Assets: BC7 SRGB
Loadscreens: BC1 sRGB (Low Quality), BC7 sRGB
Minimap: BC1 sRGB


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