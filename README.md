# junior-emulator

C256Junior emulator (Windows, Mac and Linux)

BUILDING
========

The emulator has SDL2 *development* as a dependency. In Windows this needs to be for mingw and the x64 directory (not tested with anything else) 
installed into C:\SDL2 - so there is an C:\sdl2\include c:\sdl2\bin c:\sdl2\lib and c:\sdl2\share (you can tweak this directory in documents/common.make)

Also required are mingw-gcc, python and make (not mingw32-make) (Chocolatey is the best way of installing these under Windows) and 64tass which has to 
be installed by downloading and copying the executable somewhere.

RUNNING
=======

To run use jr256 <file> <file> <file> where <file> is a filename followed by an @ followed by a load address in hex. This load address is in
the physical memory space *not* the 6502 space.

The address can be a single letter ; B (Basic ROM Location) X (Basic Code Location) M (Monitor Location) S (Sprites Location) - note the monitor
loads to the equivalent of E000 to needs to be 8k in length..

e.g. ./jr256 basic.rom@b

The kernal simply initialises and jumps to $8040. So this line loads the BASIC rom to $8000 (there is a header from 8000-803F)

The address can also be an absolute address in hexadecimal in 0x... notation.

e.g. ./jr256 hello.bin@0x001000

It is also possible to override the start address by having boot@1000 (say) in the line - which will cause it to jump to $1000. This address is in the 6502 space.

e.g. ./jr256 hello.bin@0x001000 boot@1000

To track calls and returns use the command line option 'track'

STATE
=====

Things that are implemented (mostly partially)

- Text display (including H/V scaling)
- Keyboard and Interrupts
- Bitmap
- Sprites
- Memory LUT
- Random number generator
- DMA
- Sound (under Windows, it doesn't switch off for some reason)

DEBUGGER
========

F6 enters the debugger
F1 reset
F5 run
F7 step into
F8 step over
F9 set breakpoints
TAB display screen
Type 0-9A-F to change code display, shift 0-9A-F to change data display.
