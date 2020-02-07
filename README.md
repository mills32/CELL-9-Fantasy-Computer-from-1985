# CELL-9-Fantasy-Computer-from-1985
 
FANTASY COMPUTER CELL-9 
PUBLIC INTERACTIVE COMPUTER SYSTEM
----------------------------------

This is a weird fantasy hardware, maybe it is the computer I'd have loved as a kid.
Imagine some planet in which they reached something like 1985, and people decided to 
distribute a free little pc (something like an Amiga) with a very simplified hardware and 
software, made just for creating interactive apps, like games.

Of course nearly all credits go to the creators of other fantasy computers like PICO-8.
I just wanted to create my personal PICO-8 with much more realistic "1985's pc hardware".


CPU
---
It is something like a hardware lua interpreter
This CPU can run around 512 lua instructions per frame (loop) and it is fixed at 60 fps
It can handle int and float variables, and includes math instructions like multiply, divide...

RAM
---
MAIN	1 lua script (64x256)
SOUND	16 PCM samples
		1 sequence (8 patterns 64 lines each)
PPU:	1 MAP (128x128)
		1 BKG + 1 WINDOW (16x16)
		256 tiles (5 or 17 colours)
	

INTERNAL ROM
------------
Contains the editors.
It also stores two 256 character fonts: 
	4x6 font for text and music editors.
	8x8 font for in-game text printable only in the window plane.


PPU
---
The CELL 9 has a 128x128 pixels screen and has two modes.

MODE 0
This mode can only display text and the fixed editor programs (stored in a rom chip).
Text is displayed on a plane containing 32x20 cells, and editors are generated on top of the 
text mode, by the rom program using a 128x128 framebuffer, (which is not accesible for anything 
else). Only two hardware sprites are available for the cursor and the mouse.

MODE 1
This mode provides all the necesary for the interactive apps and games.
In this mode, PPU can access 3 planes composed of tiles or cells, and 32 sprites.
Tiles are 8x8 pixels, but sprites can use 1 cell (8x8 pixels) or 4 cells (16x16 pixels).
PPU has access to 256 editable tiles, shared between planes and sprites.
	
-Plane 0: it has 16x16 cells, can be scrolled, and it wraps at the borders.
Scroll registers can be modified per scanline. This plane is always behind the others, and
due to it's small size, it can only be used for simple backgrounds.

-Plane 1: it has 128x128 cells, can be scrolled, but it does not wrap at the borders.
This plane is always on top of plane 0. Map tiles have a priority flag that can be set to be 
on top of the sprites. Scroll registers can't be modified per scanline. This plane is where 
you can store big maps for the game. 

-Plane 2: it has 16x16 cells and it can be scrolled only from -128 to 128 (x,y). This plane does not 
wrap at the borders, and it's main use is a static window to display info. CELL-9 can use the 8x8 font 
stored in ROM to print on this plane.
Plane 2 is always on top of planes 0, 1 and the sprites.

-Sprites: PPU has 32 sprites (8x8 and 16x16 pixels). They are ussualy on top of plane 1. If tiles 
from plane 1 have the priority flag set to 1, sprites will be below these tiles.
PPU can use the main cpu math to rotate sprites.

COLORS
There were two CELL-9 models:

-Model A (1985): 2 fixed palettes CGA1/CGA2 with 4 colors each + 1 transparent.
Only one palette can be used per frame.

-Model B (1986): 16 fixed colours (PICO-8) + 1 transparent. It can be set to be compatible with model A.

SPU
---
The sound processing unit has 3 melodic chanels and one sfx chanel. It can only modify volume and pitch.
There are 4Kb for 16 melodic samples and 2Kb for 8 SFX sounds. 
Each sample must be an 8 bit PCM with 256 samples each.  
There are generic samples preloaded, but you can create new ones and share them using plutonium disks.


MEDIA
-----
Plutonium rewritable carts for general storage.
Game/app carts must have this structure:

header: 5KB
scripts: 4*20 = 80KB
maps: 4*16 = 64KB
bkgs: 4*0.256 = 1KB
tilesets: 3*4 = 12KB
seqs: 4*4608 = 18KB
pcm: 4KB

180 KB


header
script_0.lua	4 lua scripts, each with 64x256 characters max. script_0 will be run first.
script_1.lua
script_2.lua
script_3.lua
map_0			4 128x128 maps, in binary format. First tile is 0.
map_1
map_2
map_3
bkg_0			4 16x16 backgrounds, in binary format. First tile is 0.
bkg_1
bkg_2
bkg_3
tset_0.png		4 tilesets (tileset_0.png - 3). 16 colors / 256 tiles. Each tile is an 8x8 pixels square.
tset_1.png
tset_2.png
tset_3.png
seq_0			4 Music sequences, in binary format. Each sequence has 8 patterns, 64 lines each.
seq_1
seq_2
seq_3
sam_0.wav		16 8 bit PCM waveforms. Each waveform has 256 samples max.
sam_1.wav
.
sam_15.wav


GET STARTED
------------

still nothing

