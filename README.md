# sauerbraten-handicap-mod a.k.a commie mod
A Mod for Cube2 Sauerbraten Collect Edition to improve gameplay for heterogenous parties using an autobalancing handicap.

The mod ensures the same rate of fragging for every player without changing result ranking. The best players will still win, but the gameplay will be less frustrating for everybody.

# Features

* New game mode 'handicap'
** Also exposed in the GUI
* Button 'lanconnect' readded to GUI
* Weapons used for a frag are shown in messages
* Mod is incompatible with original Sauerbraten in order to avoid problems
* Punch weapon damage is upgraded by a factor of 2 to encourage melee duels
* Grenade launcher damage is reduced slightly to improve weapon balance

# Game mode handicap

Whenever a player is killed, handicaps are readjusted. The current Handicap of a player influences its armour, its health, its maximum health and its attack strength.

# Inner workings of handicap mode

* Players have a new state variable `handicap`.
* Current handicaps of target (fragged) and actor (fragger) become part of the N_DIED network message.
* `handicap` is initialized to 100 for everyone at the beginning of the game.
* Spawn health and armour are corrected by the handicap. 
* Damage caused is corrected by the handicap.
* After each frag, handicaps of target and actor are recalculated on the server and health and armour are reduced accordingly.

    min_frags = minimum score of a player
    new_handicap = 100 * exp(-0.1 * (num_frags - min_frags))

** 0.1 is a factor taken from some experimenting. It is currently hard-coded into the mod and not configurable.
** This means: 
*** The exponential guarantees, that handicap will never be negative and the weakest players -- as measured by the minimum frag score -- always have handicap 100.
*** A frag margin of 10 to the weakest player translates to a handicap ratio e**1 = 2.718..., that is a handicap of 36.79....
*** A frag margin of 20 to the weakest player translates to a handicap ratio e**2 = 7.389..., that is a handicap of 13.53....
* New joiners start with a score of min_frags. Otherwise the balance would be destroyed immediately.

# Build and Run plain Sauerbraten
In order to play the mod, you have to compile sauerbraten from source after applying the provided patch.

## Linux

    curl --output sauerbraten_2013_02_03_collect_edition_linux.tar.bz2 http://downloads.sourceforge.net/project/sauerbraten/sauerbraten/2013_01_04/sauerbraten_2013_02_03_collect_edition_linux.tar.bz2
    tar xjvf sauerbraten_2013_02_03_collect_edition_linux.tar.bz2
    cd sauerbraten/src
    make clean
    make
    make install

### Prerequisites in Ubuntu 15.10

    sudo aptitude install libsdl1.2-dev libsdl-image1.2-dev libsdl-mixer1.2-dev

## Windows

* Download http://downloads.sourceforge.net/project/sauerbraten/sauerbraten/2013_01_04/sauerbraten_2013_02_03_collect_edition_windows.exe
* Install sauerbraten_2013_02_03_collect_edition_windows.exe
* Download and install TDM-GCC from http://tdm-gcc.tdragon.net/download
** as of 2016-11-01: http://sourceforge.net/projects/tdm-gcc/files/TDM-GCC%20Installer/tdm64-gcc-5.1.0-2.exe/download
* Download and install Code::Blocks from http://www.codeblocks.org/downloads
** use the version without builtin MinGW
** as of 2016-11-01: https://sourceforge.net/projects/codeblocks/files/Binaries/16.01/Windows/codeblocks-16.01-setup.exe/download

* Open Code::Blocks
* File → Open Existing Project → sauerbraten/src/vcpp/sauerbraten.cbp
* Build → Build


## Applying the patch

Just copy the contained sauerbraten/ folder over the original one and replace all files.
