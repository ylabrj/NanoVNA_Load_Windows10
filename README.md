# NanoVNA_Load_Windows10
How to update software on your NanoVNA using Windows 10 for the complete idiot.

__USE AT YOUR OWN RISK. I HAVEN'T TESTED EVERYTHING HERE BECAUSE I COVER MULTIPLE BOARD TYPES. YOU COULD BLOW YOUR BOARD AND MAKE IT UNRECOVERABLE__

Info in this page is the result of much google searching. I try to link back to the source pages in every case. Apologies if I forgot anything.

A lot of the info applies to any operating system. For the software [download steps from Linux or MacOS, check out this link](https://nt7s.com/2019/11/updating-the-nanovna-firmware/). I will refer to that page for a couple of things.

## Step 1: Which NanoVNA hardware do you have?

As of January 2020, NanoVNA has already branched into 4 hardware versions - the original __NanoVNA__, Hugen79's __NanoVNA-H__ and larger 4" display -H4; we spotted a -F variant, and being open source, there will probably be more coming.

It's not always clear which one you are getting, since some identify it on the label, some don't, and on some it's incorrect. 

When you turn on the unit, the version flashes up but disappears too quickly to read it.

To identify the version:

1. Turn on the unit
2. Tap the display to bring up the pull down menu
3. Select CONFIG
4. Select VERSION

__* Handy hint: use a stylus for tapping the screen and selecting the menus. Fat fingers don't work as well and leave fingerprints. *__

My unit says NanoVNA on the external case, but the VERSION screen identifies it as NanoVNA-H.

That first line with the github URL (in my case, **https://github.com/hugen79/NanoVNA-H**) is important. **Note it down because that tells you where to get your software updates**.

Anothe important item is the version - in my case **v0.2.3.2-g8ac9166**. That will tell you if you need to upgrade.

It's important because you need to know...

### 1A: What's the difference between the original NanoVNA and the -H? Or another version they may come up with?

Consult the github page for your board - you know, the one I told you to note down in the preceding section.

When you get to the page, don't let all the directory stuff and files at the top of the page scare you. Scroll down until you hit the README section.

ttrftech/edy55's github for NanoVNA is [here](https://github.com/ttrftech/NanoVNA) with the downloadable [software releases here](https://github.com/ttrftech/NanoVNA/releases).

hugen79's github for NanoVNA-H and -H4 is [here](https://github.com/hugen79/NanoVNA-H), with the downloadable [software releases here](https://github.com/hugen79/NanoVNA-H/releases)

For any subsequent versions, try that URL from the __CONFIG__ -> __VERSION__ page. And add **/releases** to the end of the URL on the VERSION page to get to the releases directory.

## Step 2: Download and install the DFUSE firmware converter and uploader

All NanoVNAs I've spotted so far are based on ST Micro's STM32 family of chips. Loading the firmware from your Windows PC requires ST Micro's DFuse firmware loader.

The main download page is [here](https://www.st.com/en/development-tools/stsw-stm32080.html#getsoftware-scroll) with lots of instructions.

Follow the instructions there for downloading and installing.

All the program and utilities will appear in your Windows **Start** menu under __STMicroelectronics__.

### Step 2A: Load the driver for your Windows and hardware version

Some users seem to have a problem with the DFUSE software getting loaded on their PCs, but without the appropriate driver. I had that problem too.

User [Oristo in the NanoVna forum here had the solution](https://groups.io/g/nanovna-users/topic/34550986), which I'm shamelessly copying here. The first method worked for me.

> The windows operating system needs an STMicroelectronics driver installed.
>
> __FIRST METHOD__
> 'DfuSeDemo.exe'  installed for me in a folder that also includes a 'Driver' folder,
> in which are folders for Win7-10, in each of which are subfolders for x64 and x86 (AKA 32-bit).
> In each of those driver subfolders is an installer .exe
> Run >>only<< the one that matches your Windows version and bit-depth (64 bit or 32 bit)

>  __SECOND METHOD__
> * right-click on "My PC" icon, select 'Properties'
> * select 'Device Manager'
> * attach and turn on nanoVNA, open:
>   > Ports (COM & LPT)
>- * select the appropriate COM port
>   - if you do not know which one, simply turn nanoVNA off/on to see which disappears and reappears
> * right-click and select "Update Driver Software..."  [more here] (https://www.lifewire.com/how-to-update-drivers-in-windows-2619214)
> * browse that back to the DfuSeDemo.exe installation folder

## Step 3: Which version do you want? VNA or AA? And do you need to upgrade?

__NanoVNA__ releases only one version - the VNA (Vector Network Analyser).

__NanoVNA-H__ has two versions of the software - the Vector Network Analyser (VNA) and the Antenna Analyser (AA). The devices ship with the VNA software. You need to pick which one you want. What's the difference between the two? Info on the AA version seems to be pretty sparse as of this writing (late Dec 2019). Let me know if you find something.

If you're following along properly, you have identified which NanoVNA version you have, and you know where to get the releases. If you don't, go back to the top of this page, get yourself a caffeinated beverage, drink it, and read it again.

Scrolling down on the __/releases__ page for your device, you should eventually see the release number you have on your NanoVNA. That helps confirm that you are on the right page. If you don't see it:

1. Double check in the URL: that you are on the right page for your device (NanoVNA, NanoVNA-H, etc.)
2. Check if your release number fits somewhere between a couple of release numbers on the page.

The releases on the page are the sort-of-official releases that are judged to be significant and reliable enough for release by the developers. Keeners can go right to the source and pick up interim releases to get new features early. If you purchased your NanoVNA new, it likely has one of the official releases. If you picked it up used, it may have been owned by someone smarter than me who knows how to compile and generate interim releases.


## Step 4: Pulling down the right file

Each developer releases their software differently for each board.

For Windows 10 using DFUSE, you need the firmware to be in a __.dfu__ file.

At time this was written:

* The NanoVNA release directory provides .hex and .bin files
* The NanoVNA-H release directory provides .dfu files

Follow the instructions below for the file format available for your NanoVNA.


### Example: NanoVNA: .zip file, with no .dfu
** Note**: I haven't tested this one myself, since I have a -H board. Drop me a message if there are errors. Sorry about blowing up your board.

I got some of these instructions from [here](https://docs.ghielectronics.com/hardware/loaders/stm32-bootloader.html)

The NanoVNA developer releases firmware in a .zip file that contains .hex, .bin and .elf files.

You need to convert the either the .bin or the .hex file to .dfu

Fortunately, that DFuse installation (you did that in step 2) includes a program called DFUFileMgr.exe.

* Download the .zip and unpack it.
* Start the program (from the ST Microelectronics start menu group)
* Select the appropriate conversion (*I want to GENERATE a DFU...*)

**You only need to do one of the following:**

To convert the .hex file: 
* Click the __S19 or HEX__ button. Point to the directory when you unpacked the .zip file, and go to the __build__ subdirectory
* Click on the .hex file
* Click on __Generate__ and pick a suitable file name

To convert the  .bin file
* Click on __Multi BIN__ button
* Select the .bin file from the directory where you unpacked it
* Change the address to __08000000__
* Click __Add to List__
* Click __OK__
* Click __Generate__
* Enter a name for your firmware and save the file


### Example: NanoVNA-H: Download the appropriate .dfu file

Just pick and download. Thank you hugen79 for making it easy.

## Step 5: Connect and put your NanoVNA into download mode

### 5A: Connect to USB

You'll need to connect your NanoVNA to your PC with a USB cable. Most NanoVNA ship with a good cable. If you didn't get a cable with it, be sure the USB cable you are using is good for data and not just power. *Hint: if it connects to your phone and allows you to move files back and forth, then it's a data cable.*

### 5B: Check if you can put it in download mode using the interface

More recent NanoVNA boards include a menu setting to put the board in firmware upload mode.

From the main menu on the board: __Config__, then __->DFU__ and then __Reset and Enter DFU__

If you don't see ->DFU under the Config menu, go to 5C

If you got the the DFU menu, jump to step 6

### 5C: if no ->DFU option, jumper the pins
 
 Unplug the board from the USB and power it off.
 
 [Check out this page for the proper pins to jumper](https://nt7s.com/2019/11/updating-the-nanovna-firmware/)
 
 Once the pins are jumpered, plug the board back in to the USB and power it on
 
 
 ## Step 6: Load the firmware using DFUSEdemo
 
 That's the software you loaded in Step 2.
 
 STMicroelectronics has a [great manual here on using the DFuse utilities](https://www.st.com/content/ccc/resource/technical/document/user_manual/3f/61/72/ff/c5/5a/4a/7b/CD00155676.pdf/files/CD00155676.pdf/jcr:content/translations/en.CD00155676.pdf).
 
 * Your NanoVNA should be turned on, connected by USB, and showing the firmware update screen (step 5 above)
 * Start the DFuseDemo program (Windows Start -> ST Micro -> DFuseDemo)
 * Using the pull-down under __Available DFU Devices__, select device __STM Device in DFU Mode__
  * If you do not see the device, go back to Step 2A to ensure you loaded the device driver. 
 * In the __Upgrade or Verify Action__ box, click the __Choose__ button and select the file you downloaded or converted
 * Click on __Upgrade__. You can ignore the warning message that pops up after and hit __Yes__
 * Wait for the __Upgrade Successful__ message
 * Quit
 
 Turn your NanoVNA off and on again, go to __Config__ -> __Version__ and see if the version upgraded correctly.
 
 And you're done!
 
# Information sources on using the nanoVNA
 
 ## The most comprensive user guide I have found 
 
Gunther Kraus wrote an excellent user guide and [you can find it here in a nice PDF format](http://gunthard-kraus.de/fertig_NanoVNA/English_NanoVNA_V1.5._final.pdf) that you can print, read at your leasure and scribble notes on. 

He provides an overview, detailed information on calibration, and shows the differences and advantages of using the PC interface instead of the built-in interface.

Gunther has updated the document in the past, so you may want to check his [release directory](http://gunthard-kraus.de/fertig_NanoVNA) for updated versions.
 

 ## Other links: 
 
 * HexandFlex guides to getting starting with the NanoVNA:
  * Part 1: [What is a VNA?](https://hexandflex.com/2019/08/31/getting-started-with-the-nanovna-part-1/#more-376). Includes basic setup and calibration.
  * Part 2: [Configuring Traces, Channels and Formats](https://hexandflex.com/2019/09/08/getting-started-with-the-nanovna-part-2/)
  * Part 3: [Using the NanoVNA using the VNASaver PC software](https://hexandflex.com/2019/09/15/getting-started-with-the-nanovna-part-3-pc-software/)
  
* A nice [NanoVNA case design on ThingyVerse](https://www.thingiverse.com/thing:3818979). I printed mine in ABS. Fits my NanoVNA-H perfectly.
* One of many [RTL-SDR blog entries on NanoVNA](https://www.rtl-sdr.com/tag/nanovna/). A great site for all manner of cheap and excellent radio gear.
 
 
 
 
 

 












 




