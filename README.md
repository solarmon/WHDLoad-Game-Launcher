# WHDLoad Game Launcher

# Latest release

[v0.6.1-beta](https://github.com/solarmon/WHDLoad-Game-Launcher/releases/tag/v0.6.1-beta)

Older versions can be found in [Releases](https://github.com/solarmon/WHDLoad-Game-Launcher/releases).

# Summary


![Summary Diagram](https://github.com/solarmon/WHDLoad-Game-Launcher/blob/master/WHDLoad-Game-Launcher.PNG)
      

WHDLoad Game Launcher is a startup-sequence solution for launching WHDLoad games on UAE based Amiga emulators

Two release version files are provided:

* .zip - this is the recommended directory version. Unzip this and mount as a **Directory** (DH0:) in UAE.
* .hdf - this is the legacy HDF version. Mount as a **Hardfile** (DH0:) in UAE.

Both version will need to have the appropriate kickstart ROMs put in to the **Dev/Kickstarts** directory.

# Features

* Locates the .slave file automatically - **no need to rename it to game.slave**

* **Single Slave mode**: Sinlge WHDLoad game slave file gets launched automatically.

* Supports **multiple** WHDLoad game slave files. Methods supported:
   * **Target Slave mode**: The WHDLoad game slave file selected based the Volume name of DH1:
   * **Select Slave mode**: WHDLoad game slave files selection using ABS (Amiga Boot Selector)
      * Joystick or Keyboard used for selection
* Games are launched with WHDload options from ToolTypes in the game .info file.
  - This is also saved to a .tooltypes file for each game.
  
* **Game Launcher mode**: when no WHDLoad game slave file detected a Game Launcher is launched.
     - GAMES: is assigned to DH1: (if not already assigned).
     - The game launcher can be configured to point to DH1: or GAMES: as the games repository.
* 

# Requirements and Setup

* Kickstarts - you need to put your kickstarts (including rom.key for kickstarts provided by Cloanto Amiga Forever) in the Dev/Kickstarts directory
  - See here for WHDLoad requirements: http://www.whdload.de/docs/en/need.html
  - To edit/manage the HDF file on Windows you can use ADF Opus (http://adfopus.sourceforge.net/)
  - See the the following guides for further details:
https://www.reddit.com/r/miniSNESmods/comments/8dbqv7/guide_playing_amiga_games_on_the_snes_classic/ http://lindqvist.synology.me/wordpress/?page_id=182

Or the WHDLoad Requirements page:

http://www.whdload.de/docs/en/need.html

**Note:** Cloanto kickstarts also need the rom.key copied to the same directory.

* **DH0:** is the WHDLoad boot drive. Must be writeable.
* **DH1:** is the game or games drive. Must be writeable.
* **Target Slave** and **Select Slave** - the slave file(s) must be on the root of mounted directory (DH1:). **Slave files in subdirectories are not supported**.
* Game Launcher: For WHDLoad game collections mounted on DH1: it is up to used the Game Launcher scan for games, which may include subdirectories support.
* Target Slave: based on the Volume name of DH1:
   - DH1: must be mounted as a **Directory**, nor a Hardfile (HDF)

# Target Slave mode

There needs to be a method to specify directly which slave file you want to launch.

The method used is what is called the **Target Slave** method. This method makes use of the **Volume** name of DH1:. This is explained further below.

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

# Select Slave mode

If multiple slave files are detected, and if **Target Slave** method is not used, then a selection method is used.

The selector method used is the excellent **ABS** (**Amiga Boot Selector**)

http://ohmygibs.free.fr/ohmygibs/Amiga_Boot_Selector.html

You can use the joystick or keyboard to make the selection.

The following options can be set by pressing the following keys:

* K - Change '**K**ickstart' theme
* B - Enable/Disable **B**oing **B**alls animation

AGS will remember the last settings used (stored in S:AmigaBootSelector/Options.cfg)

Up to a maximum of 12 game slave files are supported using ABS.

# Game Launcher mode

If no slave files are detected on DH1: a Game Launcher will be launched.

Currently, the excellent **TinyLauncher** is included.

http://ohmygibs.free.fr/ohmygibs/TinyLauncher.html

On first run, you will need configure it and scan for your games in DH1:, or GAMES:.

The following options can be set from the main screen by pressing the following keys:

* ESC - Exit
* F10 - Exit with return code 5
* R - Enable/disable **R**AD
* T - Enable/Disable **T**ool Types
* I - Enter **I**nfodesk
* F - Change **F**ont - Topaz or Speccy-Gibs
* H - Show **H**elp menu
* C - Enable/Disable displayt of game **C**overs / screenshots / images
* B - Boot HD / CD
* 0-4 - Set **Jump To**:
  - **0** = Disable/Enable Jump To
  - **1** = Games
  - **2** = Demos
  - **3** = Mods
  - **4** = Favourites

When in a **Jump To** screen, use **0** to enable/disable Jump To. If disabled, you can use **ESC** to go back to the main screen.

# WHDLoad

* At the moment, individual games are launched using WHDLoad and specifying the **PRELOAD** option.
* QuitKey has been set to **$59** - i.e **F10**.
  - Configurable in S/WHDLoad.prefs
* ToolTypes:
   - WHDLoad options specified as ToolTypes are recognised and used to load the game.
   - The found WHDLoad options are saved to a .tooltypes file for later/easier use. 
   
# To Do / Roadmap

* WHDload splash screen
* More Game Launchers?
  - X-bench
  - AGS
* Faster bootup, slave detection/processing and menu generation.
* Smaller footprint - remove unused commands and libraries.
* User customisation options:
  - via left/right click on bootup?
