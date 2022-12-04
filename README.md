# RZ09
Pioneer AVIC-RZ09 (for Japanese domestic market) translation

This project can be used for translation of the similar Pioneer AVIC devices (AVIC-RL09, AVIC-RW09, AVIC-RZ09, AVIC-RZ07, AVIC-RZ06, AVIC-RL05, AVIC-RZ05, AVIC-RW03, AVIC-RZ03).

And also probably can be used for other line up Pioneer AVIC devices (AVIC-RL99, AVIC-RW99, AVIC-RZ99, AVIC-RZ77, AVIC-RZ66, AVIC-RZ55, AVIC-RW33, AVIC-RZ33, AVIC-RZ22).

Thanks to @dzo for ideas and some start-up sources

## parsedat.c
Parses Japanese AVIC-RZ09 (and similar) data file initDB.dat.
Skips some dummy strings (like images, IDs, variables etc).
Writes strings "as-is" with TAB delimiter.
Fields: `<address>` `<lengh>` `<original string>`

Output file is in UCS-2 LE encoding, use Notepad++ (or other UCS-2 LE compatible editor, Chrome is OK for view strings) to see/edit results.

## translate.c

Usage: 

NOTE: You don't need to do any modification in the code, all parameters like versions and offsets will be preserved well.

Also, all parameters can be overwritten via command line parameters
translate <InitDB file name>  <Output InitDB file name> <translation file name>
the file names by defualt `initDB.dat`, `initDB_out.dat`, `translation.txt`

### Step 1:
Load strings to translate from `translation.txt` file (in UCS-2 LE encoding):
Fields: `<lenght>` `<original string>` `<translated string>` with TAB delimiter.

End of strings - Windows-based `CRLF`. 
Inside of the string's content used Unix-based `LF` new-line symbol.

### Step 2:
Open source file `initDB.dat`, search and compare source strings and size, and if similar - replace it to translated strings.
Other data blocks copied from source file to output file as-is.
Write results to `initDB_out.dat` file.

all parameters can be owerwrited via commnd line paramters
translate <InitDB file name>  <Output InitDB file name> <translation file name>
 


### translation.txt
File with some strings translated from Japanese to English. (from 4pda [https://4pda.to/forum/index.php?showtopic=847671&st=320#entry113039189] )


## patchver.c
Compile patched .NB0 file to AVIC-compatible FW file and modifiy VER and PRG files.

Usage:
 patchver  [PS140PLT.PRG] [PS140PLT.VER] [output.nb0]

Output:
`PS140PLT.PRG` - patched AVIC-platform file.
`PS140PLT.VER` - AVIC-platform version file.

# Whole process of translation 

1. Extract existing firmware from Pioneer AVIC-RZ09 from the system menu to SD-card
2. Remove first 0x200 bytes from PS140PLT.PRG by https://sourceforge.net/projects/swissfileknife/files/1-swissfileknife/1.9.8.2/]
	`sfk198.exe partcopy PS140PLT.PRG -allfrom 0x200 output.nb0 -yes`
3. Extract `initDB.dat` and use `BinMody` or `dumpromx.exe`
4. translate `initDB.dat` by `translate.exe`
	`translate.exe initDB.dat initDB_out.dat translation.txt`
5. Patch `PS140PLT.PRG' and 'PS140PLT.VER' use `patchver.exe`
    'patchver.exe PS140PLT.PRG PS140PLT.VER initDB_out.dat'
6. Replace files `PS140PLT.PRG' and 'PS140PLT.VER' on SD-card
7. Upload new firmware to AVIC-RZ09 from the system menu




