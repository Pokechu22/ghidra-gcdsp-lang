A SLEIGH processor spec for [Ghidra](https://github.com/NationalSecurityAgency/ghidra) for the GameCube/Wii DSP chip.

## Installation

This repository should be placed within the Ghidra install as the folder `Ghidra/Processors/GCDSP`, such that `Ghidra/Processors/GCDSP/data` is the path to the `data` folder.  Ghidra should automatically add it to the available processor list on its next start, and compile the files when it is first used.

## Usage

Unfortunately DSP data comes in multiple files, which makes the import process a bit complicated.

1. Select File &rarr; Import File.
2. Select a file containing DSP ucode (e.g. one dumped by Dolphin when `DumpUCode` is set to `True`).
3. Change the format to Raw Binary.
4. Select GCDSP as the language.
5. Click Options.
6. Enter "iram" as the block name, and set the base address to `inst:0000` (it defaults to `data:0000`).
7. Click OK on options, then on import, then on import results.
8. Open the imported file.
9. When prompted to analyze, click **no**.
10. Open the memory map.
11. Delete the `irom` and `coef` blocks.
12. Close the memory map.
13. Select File &rarr; Add To Program.
14. Find and select `dsp_rom.bin`.  Dolphin's [free DSP rom](https://github.com/dolphin-emu/dolphin/blob/master/Data/Sys/GC/dsp_rom.bin?raw=true) will work.
15. Change the format to Raw Binary.
16. Click Options.
17. Enter "irom" as the block name, and set the base address to `inst:8000`.
18. Click OK on options, then on add to program, then on import results.
19. Select File &rarr; Add To Program.
20. Find and select `dsp_coef.bin`.  Dolphin's [free DSP coef](https://github.com/dolphin-emu/dolphin/blob/master/Data/Sys/GC/dsp_coef.bin?raw=true) will work.
21. Change the format to Raw Binary.
22. Click Options.
23. Enter "coef" as the block name, and set the base address to `data:1000`.
24. Click OK on options, then on add to program, then on import results.
25. Select Analyzis &rarr; Auto Analyze... or press <kbd>A</kbd>.  Run analysis as normal.

## Manuals

The only manual is the [GameCube DSP User's Manual](https://github.com/dolphin-emu/dolphin/tree/master/docs/DSP/GameCube_DSP_Users_Manual), which is unfortunately incomplete.  I plan on adding to it with information I've found while working on this.

There is also documentation in Dolphin's [DSPTables.cpp](https://github.com/dolphin-emu/dolphin/blob/master/Source/Core/Core/DSP/DSPTables.cpp) and in [Dolphin's interpreter](https://github.com/dolphin-emu/dolphin/tree/master/Source/Core/Core/DSP/Interpreter).  However, DSPTables is a bit confusing to read with regards to instruction decoding, and some of the interpreter comments (e.g. those for `'LD`) are incorrect.  The code itself can also be used as a reference.
