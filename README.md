# Ghidra scripts by dojoe

Some Ghidra scripts I wrote to scratch an itch of my own that may be helpful for others too.


# `keil-ram-init.py` - Initialize RAM from Keil compressed init data

The Keil ARM toolchain stores the initialization data for .data in a
compressed block at the end of the flash binary. For static analysis
it's helpful to unpack that data and load it into the disassembler.

This script is an unpacker for that data that attempts to automatically
gather all the required data from the flash image and detect the
compression algorithm used, then splits your RAM region into an initialized,
zeroed and uninitialized one.

## Usage:

1. Create an uninitialized block called "ram" in your memory map, covering the entire SRAM of your device.
2. Find the `__scatterload` function. This is usually very easy and explained in detail in the script itself.
3. With the cursor inside the `__scatterload` function, launch the script.
4. OPTIONAL: If step 3 doesn't work, you can select the control table by hand to help the script along.

See the initial comment block in the script for details.


# `keil-decompress.py` - Decompress a Keil compressed memory block

If `keil-ram-init.py` doesn't work for some reason you may have to figure out the
memory initialization yourself. To help you with that here's a script that will take
care of the decompression step by simply marking the compressed data and running
the script. The decompressed data will be placed into the clipboard.

See the initial comment block in the script for detailed instructions.
