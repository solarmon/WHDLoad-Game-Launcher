# WHDLoad-Game-Launcher

A boot up solution for launching WHDLoad games for UAE based Amiga emulators

Two release version files are provided:

* .zip - this is the recommended **Directory** version. Unzip this and mount as a directory (DH0:) in UAE.
* .hdf - this is the legacy HDF version

Both version will need to have the appropriate kickstart ROMs put in to the **Dev/Kickstarts** directory.

# Features

* Locates the slave file automatically - no need to rename it to game.slave
* Detects multiple WHDLoad game slave files
   * WHDLoad game slave file selected based the volume name of DH1:
   * WHDLoad game slave file selection via a selection dialogue.
* Single WHDLoad game slave file just gets launched normally.
* When no WHDLoad game slave file detected
   * A game launcher is launched.
     - GAMES: is assigned to DH1: (if not already assigned).
     - The game launcher can be configured to point to DH1: or GAMES: as the games repository.
* WHDload options from Tool Types support if a previously generated .tooltypes file is present.

# Requirements

* Kickstarts - you need to put your kickstarts (including rom.key for kickstarts provided by Cloanto Amiga Forever) in the Dev/Kickstarts directory
  - To edit/manage the HDF file on Windows you can use ADF Opus (http://adfopus.sourceforge.net/)
  - See the the following guides for further details:
https://www.reddit.com/r/miniSNESmods/comments/8dbqv7/guide_playing_amiga_games_on_the_snes_classic/ http://lindqvist.synology.me/wordpress/?page_id=182

* DH0: is the WHDLoad boot drive
* DH1: is the game or games drive
* For indivudal WHDLoad (in a directory, not in a .hdf file) games, the slave file(s) must be on the root of mounted directory (DH1:). Subdirectories are not supported.
* For WHDLoad game collections mount on DH1: it is up to the game launcher scan for games, including subedirectories.
* WHDLoad game slave file as DH1: volume name:
   - DH1: must be mounted as a Directory, nor a Hardfile (HDF)

# WHDLoad Game Slave file as Volume Name

There are several hard drive formats supported by UAE:

* Directory
* Hardfile (HDF)
* Archive
* Plain File

The first two are generally the preferred/typical methods.

However, when a **Hardfile** HDF file is used, the **volume name** is taken from insde the .hdf file and not the actual filename. When a HDF file is created (for example, usoing ADF Opus) you specify the volume name for it.

When a **Directory** (or **Archive** or **Plain File**) is used, you **can** specify the volume name.

Thus, if you have multiple game slave files in your WHDL game partition and want to specify the game slave version to launch, the WHDLoad game must be mounted as a **Directory** and the slave file name provided as the volume name. Otherwise, a selection dialogue will be used to ask the user to select a game slave file to launch.

**It is also recommended that both the WHDLoad DH0: and Game/Games DH1 partition are mount as as a directories - it just makes make changes to them much easier on the host emaulation system.**

# WHDLoad

* At the moment, individual games are launched using WHDLoad and specifying the **PRELOAD** option.
* QuitKey has been set to $59 - i.e F10.
* Tooltypes:
   - If a .tooltypes file is found for the slave file, the options found in this will be used to launch the game.
   - Some WHDLoad game launchers automatically generate the .tooltypes for each game slave it finds.

# Game Launcher

Currently, the excellent **TinyLauncher* is included.

http://ohmygibs.free.fr/ohmygibs/TinyLauncher.html

On first run, you will need configure it and scan for your games in DH1:, or GAMES:

# To Do / Roadmap

* Better ToolTypes support?
   - Need to support tooltyoes natively - via the .info icon file, and not via .tooltypes file?
   - Maybe use **kgiconload**?
   - Or method to extract the tooltypes values on the fly?
   - Some WHDLoad launchers support tooltypes - but need NewIcons support?
* Better multiple game slave selector:
   - Use ABS (Amiga Boot Selector)?
* More Game Launchers?
  - X-bench
  - AGS
