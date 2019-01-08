# WHDLoad-Game-Launcher

A boot up solution for launching WHDLoad games for UAE based Amiga emulators

The startup process use supports:

* Multiple game slave files
 * Game slave file selection by a user choice dialogue.
 * Game slave file selected based the volume name of DH1:
   - Note: This requires for the UAE emulator to mount the drive and set the slave file name as the volume name of DH1:
* Single game slave file:
  * Just launch it normally.
* No game slave file
  * A game launcher and can be run.
    - The game launcher can be configured to point to DH1: as the games repository.

Assumptions:

* DH0: is the boot drive
* DH1: is the game or games drive

