# WHDLoad Game Launcher

# Latest release

[v0.8-beta](https://github.com/solarmon/WHDLoad-Game-Launcher/releases/tag/v0.8-beta)

Older versions can be found in [Releases](https://github.com/solarmon/WHDLoad-Game-Launcher/releases).

# Summary

WHDLoad Game Launcher is a startup-sequence solution for launching WHDLoad games on UAE based Amiga emulators

It supports three modes of operation:

* Slave Target - to target a specific slave file.
* Slave Selection - to select from multiple slave files.
* Slave Collection - to use a Game Launcher for your games collection.

As summary of the setup and options can be seen below:


![Summary Diagram](https://github.com/solarmon/WHDLoad-Game-Launcher/blob/master/WHDLoad-Game-Launcher.PNG)


Two release versions are provided:

* .zip - this is the recommended directory version. Unzip this and mount as a **Directory** (DH0:) in UAE.
* .hdf - this is the legacy HDF version. Mount as a **Hardfile** (DH0:) in UAE.

# Features

* Locates the .slave file automatically - **no need to rename it to game.slave**
  - If a game.slave file is detected a warning is displayed.

* **Single Slave mode**: Sinlge WHDLoad game slave file gets launched automatically.

* Supports **multiple** WHDLoad game slave files. Methods supported:
   - **Slave Target mode**: The WHDLoad game slave file selected based the Volume name of DH1:
     - This mode is **not** supported when DH1: is mounted with a **.lha** or **.zip** WHDLoad game file.
   - **Slave Selection mode**: WHDLoad game slave files selection using **ABS** (Amiga Boot Selector)
      * **Joystick** or **Keyboard** used for selection

* Games are launched with WHDload options from **ToolTypes** in the game **.info** file.
  
* **Slave Collection mode**: when no WHDLoad game slave file detected a Game Launcher is launched.
     - **GAMES:** is assigned to DH1: (if not already assigned).
     - The game launcher can be configured to point to DH1: or GAMES: as the games repository.

* **Workbench mode**: A minimal Workbench is loaded at the end, after game exit (use F10).
  - Multiview can be used to view readme, guides, solutions, etc documents.
  - Files and directories can be managed and renamed - i.e. rename the game.slave file.

# Requirements

See the diagram above for reference.

* WinUAE emulator
  - but other UAE based emulators may work!
  
* Kickstarts:
  - For boot up: Kickstart 3.1
  - For WHDLoad: various - game dependent
  - rom.key if you are using Cloanto Kickstarts.
  - See here for WHDLoad requirements: http://www.whdload.de/docs/en/need.html

* To edit/manage the HDF file on Windows you can use ADF Opus (http://adfopus.sourceforge.net/)
  - See the the following guides for further details:
  https://www.reddit.com/r/miniSNESmods/comments/8dbqv7/guide_playing_amiga_games_on_the_snes_classic/
  http://lindqvist.synology.me/wordpress/?page_id=182

  - Or the WHDLoad Requirements page:
  http://www.whdload.de/docs/en/need.html
 
 * WHDLoad Game
   - Get them from https://www.whdownload.com/
   - The game name for the **.info** and **.slave** files **MUST match exactly**.
   - UAE drive mount formats:
     - Directory
     - .hdf
     - .lha / .zip
       - DH1: drive is READ ONLY
       - Games saves cannot be written to DH1:
       - SavePath WHDLoad option enabled to allow games saves to DH0:WHDSaves
       - (Tested on WinUAE)

# Setup

See the diagram above for reference.

* **DH0:** is the WHDLoad boot drive. Must be writeable.
  - You need to put your kickstarts (including rom.key for Cloanto Amiga Forever kickstarts) in the **System:Dev/Kickstarts** directory

* **DH1:** is the game or games drive. Must be writeable.
  - **Slave Target** mode:
    - DH1: must be mounted as a **Directory** and the Volume name set to target slave file name.
    - Slave file) must be in the root of DH1:
     - **Slave files in subdirectories are not supported**.
  - **Slave Selection** mode:
    - DH1: can be mounted as a Directory or HDF
    - Slave files must be in the root of DH1:
    - **Slave files in subdirectories are not supported**.
  - **Slave Collection** mode:
    - The game collection must be mounted on DH1: it is up to the Game Launcher to scan for games, which may include subdirectories support.
  - For .lha / .zip files mounted on DH1:
    - DH1: becomes READONLY
    - The Volume name must be in the following format:
      \<GameDirName\>.\<ext\>
      Where \<GameDirName\> is the game subdirectory in the .lha or .zip file.
      Where \<ext\> is the compression extension - either .lha or .zip
    - The Volume name, including the extension cannot exceed 30 characters.
    - WHDLoad option **SavePath=SYS:WHDSaves** is added to allow save games to **DH0:WHDSaves**


# Slave Target mode

There needs to be a method to specify directly which slave file you want to launch.

The method used is what is called the **Slave Target** method. This method makes use of the **Volume** name of DH1:. This is explained further below.

There are several hard drive formats supported by UAE:

* Directory
* Hardfile (HDF)
* Archive
* Plain File

The first two are generally the preferred/typical methods.

However, when a **Hardfile** HDF file is used, the **volume name** is taken from inside the .hdf file and not the actual filename. When a HDF file is created (for example, using ADF Opus) you specify the volume name for it.

When a **Directory** (or **Archive** or **Plain File**) is used, you can manually specify the volume name.

Thus, if you have multiple game slave files in your WHDL game partition and want to specify the game slave file to launch, the WHDLoad game must be mounted as a **Directory** and the game slave file name (including the .slave extension) is used as the volume name. Otherwise, a selection dialogue will be used to ask the user to select a game slave file to launch.

**It is also recommended that both the WHDLoad boot DH0: and the Game/Games DH1: partition are mounted as as a directories - it just allows managing them much easier on the host emulation system**

# Slave Selection mode

If multiple slave files are detected, and if **Slave Target** method is not used, then a selection method is used.

The selector method used is the excellent **ABS** (**Amiga Boot Selector**)

http://ohmygibs.free.fr/ohmygibs/Amiga_Boot_Selector.html

You can use the joystick or keyboard to make the selection.

The following options can be set by pressing the following keys:

* K - Change '**K**ickstart' theme
* B - Enable/Disable **B**oing **B**alls animation

AGS will remember the last settings used (stored in S:AmigaBootSelector/Options.cfg)

Up to a maximum of 12 game slave files are supported using ABS.

# Slave Collection mode

If no slave files are detected on DH1: a Game Launcher will be launched.

Currently, the excellent **TinyLauncher** is included.

http://ohmygibs.free.fr/ohmygibs/TinyLauncher.html

On first run, you will need configure it and scan for your games in DH1:, or GAMES:.

The following options can be set from the main screen by pressing the following keys:

* ESC - Exit
* F10 - Exit with return code 5
* A (on AZERTY keyboards) - **A**dd to Favorites (in Game memu)
* Q (on QWERTY keyboards) - **A**dd to Favorites (in Game memu) 
* D - **D**elete from Favorites (in Favorites menu)
* R - Enable/disable **R**AD
* T - Enable/Disable **T**ool Types
* I - Enter **I**nfodesk
* F - Change **F**ont - Topaz or Speccy-Gibs
* H - Show **H**elp menu
* C - Enable/Disable display of game **C**overs / screenshots / images
* B - Boot HD / CD
* 0-4 - Set **Jump To**:
  - **0** = Disable/Enable Jump To
  - **1** = Games
  - **2** = Demos
  - **3** = Mods
  - **4** = Favourites

When in a **Jump To** screen, use **0** to enable/disable Jump To. If disabled, you can use **ESC** to go back to the main screen.

# WHDLoad

* QuitKey has been set to **$59** - i.e **F10**.
  - Configurable in S/WHDLoad.prefs
* ToolTypes:
   - WHDLoad options specified as ToolTypes are recognised and used to load the game.

# To Do / Roadmap

* Parsing info using UAE config file
  - This will allow more info to be passed (avoiding 30 character limit of Volume name)
  - Use uae-configuration during startup-sequence to read custom UAE config entries.
* More Game Launchers?
  - X-bEnCh (http://www.jimneray.com/xbench.html)(http://eab.abime.net/showthread.php?t=65633)
  - AGS2 (https://github.com/MagerValp/ArcadeGameSelector)(http://eab.abime.net/showthread.php?t=68818)
  - KGLoad (http://eab.abime.net/showthread.php?t=66086)
* Faster bootup, slave detection/processing and menu generation.
* Smaller footprint - remove unused resources.
* User customisation options:
  - via left/right mouse button on bootup?
  - Joystick input?
  
  # Credits and links

* WHDLoad Game Launcher was developed and tested in WinUAE.
  - http://www.winuae.net/
* The excellent WHDLoad boot setup guides at:
  - https://www.reddit.com/r/miniSNESmods/comments/8dbqv7/guide_playing_amiga_games_on_the_snes_classic/
  - http://lindqvist.synology.me/wordpress/?page_id=182
 * The WHDLoad team:
   - http://whdload.de/
 * Michael Gibs for his TinyLauncher and ABS programs:
   - http://ohmygibs.free.fr/ohmygibs/TinyLauncher.html
   - http://ohmygibs.free.fr/ohmygibs/Amiga_Boot_Selector.html
 * ADF Opus - for creating .hdf files
   - http://adfopus.sourceforge.net/
 * Additional programs, tools and libraries used:
   - rexxtricks.library - http://aminet.net/package/util/rexx/RexxTricks_386
   - GetVolumeName - http://aminet.net/package/util/cli/GetVolumeName
   - JoyMouse - http://aminet.net/package/util/mouse/JoyMouse
   - kgiconload - http://eab.abime.net/showpost.php?p=584390&postcount=72
   - WBRun - http://aminet.net/package/util/cli/WBRun
   - bblank - http://aminet.net/package/util/boot/BBlank
