# RZ09
Pioneer AVIC-RZ09 (for Japanese domestic market) translation

This project can be used for translation of the similar Pioneer AVIC devices (AVIC-RL09, AVIC-RW09, AVIC-RZ09, AVIC-RZ07, AVIC-RZ06, AVIC-RL05, AVIC-RZ05, AVIC-RW03, AVIC-RZ03)
And also probably can be used for other line up Pioneer AVIC devices (AVIC-RZ77, AVIC-RZ06, AVIC-RZ55, AVIC-RW33, AVIC-RZ33, AVIC-RZ22)

Thanks to @dzo for ideas and some start-up sources

## parsedat.c
Parses Japanese AVIC-RZ09 (and similar) data file initDB.dat.
Skips some dummy strings (like images, IDs, variables etc).
Writes strings "as-is" with TAB delimiter.
Fields: `<address>` `<lengh>` `<original string>`

Output file is in UCS-2 LE encoding, use Notepad++ (or other UCS-2 LE compatible editor, Chrome is OK for view strings) to see/edit results.

### parsed104_with_addr.txt
Example of parsed initDB.dat (ver.1.04 of AVIC-RZ09).

## translate.c

### Step 1:
Load strings to translate from `translation.txt` file (in UCS-2 LE encoding):
Fields: `<lenght>` `<original string>` `<translated string>` with TAB delimiter.

End of strings - Windows-based `CRLF`. 
Inside of the string's content used Unix-based `LF` new-line symbol.

### Step 2:
Open source file `initDB.dat`, search and compare source strings and size, and if similar - replace it to translated strings.
Other data blocks copied from source file to output file as-is.
Write results to `initDB_out.dat` file.

### translation.txt
File with some strings translated from Japanese to English.

### parsed104_tr_all.txt
File with all Japanese strings, extracted from `initDB.dat`, translated by Google Translator and saved "as-is".

## makever.c
Compile patched .NB0 file to AVIC-compatible FW file.

Input:
`fw_104.nb0` - pathced .NB0 file.

Output:
`PS140PLT.PRG` - patched AVIC-platform file.
`PS140PLT.VER` - AVIC-platform version file.
