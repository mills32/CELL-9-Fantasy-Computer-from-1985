# CELL-9-Fantasy-Computer-from-1985
 
## FANTASY COMPUTER CELL-9 PUBLIC INTERACTIVE COMPUTER SYSTEM

This is a weird fantasy hardware, maybe it is the computer I'd have loved as a kid.
Imagine some planet in which they reached something like 1985, and people decided to 
distribute a free little pc (something like an Amiga) with a very simplified hardware and 
software, made just for creating interactive apps, like games.

Of course nearly all credits go to the creators of other fantasy computers like PICO-8.
I just wanted to create my personal PICO-8 with much more realistic "1985's pc hardware".


## 1 CPU
It is something like a hardware lua interpreter
This CPU can run around 512 lua instructions per frame (loop) and it is fixed at 60 fps
It can handle int and float variables, and includes math instructions like multiply, divide...


## 2 RAM
MAIN:   
- 1 lua script (64x256)  

SOUND:  
- 16 PCM samples + 8 SFX  
- 1 sequence (8 patterns 64 lines each)  

PPU:  
- 1 MAP (128x128)  
- 1 BKG + 1 WINDOW (16x16)  
- 256 tiles (5 or 17 colours)  	
  
  
## 3 INTERNAL ROM
Contains the editors.
It also stores two 256 character fonts: 
- 4x6 font for text and music editors.
- 8x8 font for in-game text printable only in the window plane.


## 4 PPU
The CELL 9 has a 128x128 pixels screen and has two modes.
#### PPU MODE 0
This mode can only display text and the fixed editor programs (stored in a rom chip).
Text is displayed on a plane containing 32x20 cells, and editors are generated on top of the 
text mode, by the rom program using a 128x128 framebuffer, (which is not accesible for anything 
else). Only two hardware sprites are available for the cursor and the mouse.
#### PPU MODE 1
This mode provides all the necesary for the interactive apps and games.
In this mode, PPU can access 3 planes composed of tiles or cells, and 32 sprites.
Tiles are 8x8 pixels, but sprites can use 1 cell (8x8 pixels) or 4 cells (16x16 pixels).
PPU has access to 256 editable tiles, shared between planes and sprites.	
- Plane 0:  
It is a 16x16 cell Map, can be scrolled, and it wraps at the borders.
Scroll registers can be modified per scanline. This plane is always behind the others, and
due to it's small size, it can only be used for simple backgrounds.
- Plane 1:  
It is a 128x128 cell map, can be scrolled, but it does not wrap at the borders.
This plane is always on top of plane 0. Map tiles have a priority flag that can be set to be 
on top of the sprites. Scroll registers can't be modified per scanline. This plane is where 
you can store big maps for the game. 
- Plane 2:  
It is a 16x16 cell map and it can be scrolled only from -128 to 128 (x,y). This plane does not 
wrap at the borders, and it's main use is a static window to display info. CELL-9 can use the 8x8 font 
stored in ROM to print on this plane. Plane 2 is always on top of planes 0, 1 and the sprites.  
- Sprites:  
PPU has 32 sprites (8x8 and 16x16 pixels). They are ussualy on top of plane 1. If tiles 
from plane 1 have the priority flag set to 1, sprites will be below these tiles.
PPU can use the main cpu math to rotate sprites.  
  
#### PPU COLORS
There were two CELL-9 models:
- Model A (1985): 2 fixed palettes CGA1/CGA2 with 4 colors each + 1 transparent.
Only one palette can be used per frame.
- Model B (1986): 16 fixed colours (PICO-8) + 1 transparent. It can be set to be compatible with model A.  
  
  
## 5 SPU
The sound processing unit has 3 melodic chanels and one sfx chanel. It can only modify volume and pitch.
There are 4Kb for 16 melodic samples and 2Kb for 8 SFX sounds. 
Each sample must be an 8 bit PCM with 256 samples each.  
There are generic samples preloaded, but you can create new ones and share them using plutonium disks.  
  
  
## 6 MEDIA
Plutonium rewritable carts for general storage.  
Game/app carts must have this structure: 
  
4 lua scripts: each with 64x256 characters max. script_0 will be run first.  
4 128x128 maps: in binary format. First tile is 0.  
4 16x16 backgrounds: in binary format. First tile is 0.  
4 tilesets: 17 colors / 256 tiles. Uncompressed PNG.  
4 Music sequences, in binary format. Each sequence has 8 patterns, 64 lines each.  
24 waveforms. Each waveform is an 8 bit PCM, and has 256 samples max.  
  
Cartridges are 240KB:  
scripts: 4x20 = 80KB  
maps: 4x16 = 64KB  
bkgs: 8x0.256 = 2KB  
tilesets: 4x16 = 64KB  
seqs: 4x6 = 24KB  
sam: 24x0.256 = 6KB  
   
script_0.lua    
script_1.lua  
script_2.lua  
script_3.lua  
map_0  
map_1  
map_2  
map_3  
bkg_0  
bkg_1  
bkg_2  
bkg_3  
tset_0.png  
tset_1.png  
tset_2.png  
tset_3.png  
seq_0  
seq_1  
seq_2  
seq_3  
sam_0.wav  
sam_1.wav  
...  
sam_23.wav  
  
  
## 7 HADR DISK
The computer has an internal 256KB storage with the same structure as the external cart, but empty. Here you can create your app and them save it to the external cart.
  
  
## GET STARTED
still nothing

