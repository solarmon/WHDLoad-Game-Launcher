# WHDLoad-Game-Launcher

A boot up solution for launching WHDLoad games for UAE based Amiga emulators

# Features

* Multiple WHDLoad game slave files
   * WHDLoad game slave file selected based the volume name of DH1:
   * WHDLoad game slave file selection via a user choice dialogue.
* Single WHDLoad game slave file:
   * Just gets launched normally.
* No WHDLoad game slave file
   * A game launcher is launched.
     - GAMES: is assigned to DH1: (if not already assigned).
     - The game launcher can be configured to point to DH1: or GAMES: as the games repository.

# Requirements

* DH0: is the boot drive
* DH1: is the game or games drive
* For indivudal WHDLoad games (including single and multiple game slaves) the slave files must be on the root of DH1:
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

Thus, if you have multiple game slave files in your WHDL game partition and want to specify the game slave version to launch, the WHDLoad game must be mounted as a **Directory**. Otherwise, a user selection dialogue will be used to ask the user to select a game slave file to launch.

# WHDLoad

* At the moment, individual games are launched using WHDLoad and specifying the **PRELOAD** option.
* QuitKey has been set to $59 - i.e F10.
* Tooltypes:
   - If a .tooltypes file is found for the slave file, the options found in this will be used to launch the game.
   - Some WHDLoad game launchers automatically generate the .tooltypes for each game slave it finds.

# To Do / Roadmap

* ToolTypes support
   - Need to support tooltyoes natively - via the .info icon file, and not via .tooltypes file?
   - Maybe use **kgiconload**?
   - Or method to extract the tooltypes values on the fly?
   - Some WHDLoad launchers support tooltypes - but need NewIcons support?
* Better multiple game slave selector:
   - ABS (Amiga Boot Selector)? 
