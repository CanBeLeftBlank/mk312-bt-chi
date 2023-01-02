Welcome to the MK-312BTχ (Chi) project. This is a fork of the project bij [CrashOverride85](https://github.com/CrashOverride85/mk312-bt) which itself is cloned from an earlier project and ultimately a project by MetaFetish that has since been removed from GitHub.

# What is it?

MK-312BTχ is a DYI electronics kit to build an Estim box, including schematics, printed circuit board layouts and parts lists. If you don't know what an Estim box is or have no experience with electronics and soldering, this project is probably not for you...

If you do know what an Estim box is: build and use at your own risk! Even though a lot of people have build these devices there's always room for error and (painful) experiences.

## How is this different from the other cloned projects?

The original designs were made with the Eagle CAD software. Since I don't have an expensive Eagle license I decided to convert the schematics to the open source KiCad format. This will hopefully allow more people to experiment with this or improve the design.

There was also an update available of the schematic (v1.4) and final board design, but only as PDFs and images. So I compared them with the old v1.3 Eagle designs and re-applied the changes in the KiCad version. This is the original v1.4χ version.

Second, documentation was always a bit lacking or confusing. This project aims to improve on that.

And who knows, maybe in the future we'll have original source code and firmware as well...

## What's with the X in the version?

It's not an X but the Greek letter χ (Chi) which is pronounced 'Kai', similar to 'KiCad'. 


# Building!

So, let's get to the main event. There are 4 parts to this:

* Getting the circuit boards
* Buying the electronic parts
* Soldering and putting it together
* Programming the firmware

Oh yes, before you continue: you must be able to program an Atmel microcontroller or have someone who can do it for you. 

## Circuit boards (PCB)

In the gerbers/ folder are the latest Gerber files as zip files, one for each of the 3 boards: the main circuit board, the display print and the front panel. Easiest is to have these boards made at a PCB factory; the front panel looks best with a black soldermask.

The zip files contain Gerber files with Protel filenames; they are known to work with at least one PCB manufacturer (PCBWay: no affiliation or sponsorship). I would like some feedback on how it fares with other manufacturers.


## The electronic parts

*As of the time of writing (December 2022), there is still a global shortage of chips and other electronic parts. However, with a little bit of creativity you can still get all the parts. For example I substituted the main processor, an ATMega16A-PU, with the ATMega16L-8PU, a low-power version that runs 'only' at 8 MHz which so happens to be the actual clockspeed. The stereo pot at the display panel is no longer available at Mouser, but AliExpress has plenty of them. And the blue LCD that is originally specified is not shipped everywhere, so I picked a green one.*

In the bom_and_info/ folder is a spreadsheet with a parts-list for Mouser; a few substitutions / replacements have been marked with colors and notes. This list has been used to get parts in August 2022, but your milage may vary. There is no BOM for other parts suppliers, but all components are standard parts so it should be easy to find them. The BOM also contains a suitable case.

There is one choice you have to make: which transformer to use. The PCB supports two types: the Xicon 42TL004 (default) and the 42TU200. The latter is bigger and should give more power on the outputs, but was until recently only available in bulk. If you buy the 42TU200 you must use a lower value for R30; see the BOM for details.

You need a short ribbon cable to connect the display to the main board. The BOM lists separate components for this but you can also buy a pre-made 24-pin ribbon cable at Amazon, EBay or AliExpress.

## Building it

In the bom_and_info/ folder there is a document with detailed building instructions, as well as 2 PDFs with component placements for the display and mainboard. You will need a soldering iron with a fine tip, some thin solder (leaded or lead-free) and a bit of free time. All parts are through-hole so easy to mount. 

With the given PCBs and case you can mount the mainboard at the bottom of the case with a few short screws; the display with front panel slides in vertically (see the images). 

## Programming the firmware

This is a bit of a gray area. There are various firmware revisions floating around on the 'Net, sometimes with names like 'buttshock'; problem is they are only available as binary files, no sources. Some have patches and fixes to the original firmware but are still binary-only. 

This repository contains an old but working version of the firmware with tweaks for the chosen LCD; this has to do with the ← and → symbols on the LCD that differs between brands.

To set your programmer fuses:

* Low fuse: 0xFF
* High fuse: 0xDC

This assumes an 8 MHz crystal is used.

On the mainboard PCB is a 6-pin header for programming, compatible with the Atmel-ICE programmer (and probably a few others). An alternative is an external programmer. There is no way to upload the firmware using a bootloader AFAIK.

# Using it

## Charging

The recommende charging voltage is 15 Volt DC; the box monitors the input voltage and if it is too high, the firmware may display an error 21. The battery will still be charged to its nominal voltage but the LM2914 might get hot due to a high charging current.

Note: as with all estim boxes it is not recommend to use the machine while it is being charged and thus (indirectly) connected to mains voltage.
