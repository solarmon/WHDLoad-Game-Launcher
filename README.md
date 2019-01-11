# WHDLoad Game Launcher

# Latest release

[v0.5-beta](https://github.com/solarmon/WHDLoad-Game-Launcher/releases/tag/v0.5-beta)

Older versions can be found in [Releases](https://github.com/solarmon/WHDLoad-Game-Launcher/releases).

# Summary

WHDLoad Game Launcher is a startup-sequence solution for launching WHDLoad games on UAE based Amiga emulators

Two release version files are provided:

* .zip - this is the recommended **Directory** version. Unzip this and mount as a directory (DH0:) in UAE.
* .hdf - this is the legacy HDF version

Both version will need to have the appropriate kickstart ROMs put in to the **Dev/Kickstarts** directory.

# Features

* Locates the slave file automatically - no need to rename it to game.slave
* Supports multiple WHDLoad game slave files
   * Target Slave: The WHDLoad game slave file selected based the Volume name of DH1:
   * Slave Selector: WHDLoad game slave files selection via ABS (Amiga Boot Selector)
      * Joystick or Keyboard used for selection
* Single WHDLoad game slave file just gets launched normally.
* When no WHDLoad game slave file detected
   * A game launcher is launched.
     - GAMES: is assigned to DH1: (if not already assigned).
     - The game launcher can be configured to point to DH1: or GAMES: as the games repository.
* WHDload options from Tool Types supported if a separately generated .tooltypes file is present.

# Requirements and Setup

* Kickstarts - you need to put your kickstarts (including rom.key for kickstarts provided by Cloanto Amiga Forever) in the Dev/Kickstarts directory
  - See here for WHDLoad requirements: http://www.whdload.de/docs/en/need.html
  - To edit/manage the HDF file on Windows you can use ADF Opus (http://adfopus.sourceforge.net/)
  - See the the following guides for further details:
https://www.reddit.com/r/miniSNESmods/comments/8dbqv7/guide_playing_amiga_games_on_the_snes_classic/ http://lindqvist.synology.me/wordpress/?page_id=182

* **DH0:** is the WHDLoad boot drive
* **DH1:** is the game or games drive
* For indivudal WHDLoad (in a directory, not in a .hdf file) games, the slave file(s) must be on the root of mounted directory (DH1:). **Slave files in subdirectories are not supported**.
* Game Launcher: For WHDLoad game collections mounted on DH1: it is up to used the Game Launcher scan for games, which may include subdirectories support.
* Target Slave: based on the Volume name of DH1:
   - DH1: must be mounted as a **Directory**, nor a Hardfile (HDF)

# WHDLoad

* At the moment, individual games are launched using WHDLoad and specifying the **PRELOAD** option.
* QuitKey has been set to **$59** - i.e **F10**.
  - Configurable in S/WHDLoad.prefs
* Tooltypes:
   - If a **.tooltypes** file is found for the slave file, the options found in this will be used to launch the game.
   - Some WHDLoad game launchers automatically generate the .tooltypes for each game slave it finds.

# Multiple Slaves: Target Slave

There needs to be a method to specify directly which slave file you want to launch.

The method I have used is what I call the **Target Slave** method is to make use of the Volume name of DH1:, which is explained below.

There are several hard drive formats supported by UAE:

* Directory
* Hardfile (HDF)
* Archive
* Plain File

The first two are generally the preferred/typical methods.

However, when a **Hardfile** HDF file is used, the **volume name** is taken from insde the .hdf file and not the actual filename. When a HDF file is created (for example, using ADF Opus) you specify the volume name for it.

When a **Directory** (or **Archive** or **Plain File**) is used, you can manually specify the volume name.

Thus, if you have multiple game slave files in your WHDL game partition and want to specify the game slave version to launch, the WHDLoad game must be mounted as a **Directory** and the slave file name (including the .slave extension) provided as the volume name. Otherwise, a selection dialogue will be used to ask the user to select a game slave file to launch.

**It is also recommended that both the WHDLoad DH0: and Games (collections) DH1: partition are mounted as as a directories - it just allows managing them much easier on the host emulation system, and you do not have to worry about the size of the .hdf file**

# Multiple Slaves: Slave Selector

If multiple slave files are detected and if the **Target Slave** method is not used, then a selector menu is provided.

The selector menu used is the excellent **ABS** (**Amiga Boot Selector**)

http://ohmygibs.free.fr/ohmygibs/Amiga_Boot_Selector.html

You can use the joystick or keyboard to make the selection.

The following options can be set by pressing the following keys:

K - Change '**K**ickstart' theme
B - Enable/Disable **B**oing **B**alls animation

AGS will remember the last settings used (stored in S:AmigaBootSelector/Options.cfg)


# Game Launcher

If no slave files are detected on DH1: a Game Launcher will be launched.

Currently, the excellent **TinyLauncher** is included.

http://ohmygibs.free.fr/ohmygibs/TinyLauncher.html

On first run, you will need configure it and scan for your games in DH1:, or GAMES:.

The following options can be set from the main screen by pressing the following keys:

ESC - Exit
F10 - Exit with return code 5
R - Enable/disable **R**AD
T - Enable/Disable **T**ool Types
I - Enter **I**nfodesk
F - Change **F**ont - Topaz or Speccy-Gibs
H - Show **H**elp menu
C - Enable/Disable displayt of game **C**overs / screenshots / images
B - Boot HD / CD
0-4 - Set **Jump To**:
  - **0** = Disable/Enable Jump To
  - **1** = Games
  - **2** = Demos
  - **3** = Mods
  - **4** = Favourites

When in a Jump To scree, use **0** to enable/disable Jump To. If disabled, you can use **ESC** to go back to the main screen.

# To Do / Roadmap

* Better ToolTypes support?
   - Need to support tooltyoes natively - via the .info icon file, and not via .tooltypes file?
   - Maybe use **kgiconload**?
   - Or method to extract the tooltypes values on the fly?
   - Some WHDLoad launchers support tooltypes - but need NewIcons support?
* More Game Launchers?
  - X-bench
  - AGS
* Faster bootup, slave detection and menu generation.
