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
//					Visibility Flags					 //
//=========================================================

visibilityflags:
    opaque: your material will be opaque.
    transparent: your material will be transparent, this does not work out of the box currently.
    colpass: use this if it's a colpass material.
    none: use this if it's a loadscreen material.

faceflags:
    6: normal outward drawing faces
    7: outward drawing faces, but wireframe.


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
//					Useful Shadersets 					 //
//=========================================================

WLDC: 3134464214606249681 (Makes textures redish, used for Mirage Voyage)
WLDC: 5455669381027863835 (Makes material glow)
SKNP: 8900632333082111100 (Glossy weapon shaderset)


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