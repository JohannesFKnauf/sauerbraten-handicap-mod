# sauerbraten-handicap-mod
A Mod for Cube2 Sauerbraten Collect Edition to improve gameplay for heterogenous parties using an autobalancing handicap.

# Build and Run plain Sauerbraten
In order to play the mod, you have to compile sauerbraten from source.

## Linux

    curl --output sauerbraten_2013_02_03_collect_edition_linux.tar.bz2 http://downloads.sourceforge.net/project/sauerbraten/sauerbraten/2013_01_04/sauerbraten_2013_02_03_collect_edition_linux.tar.bz2
    tar xjvf sauerbraten_2013_02_03_collect_edition_linux.tar.bz2
    cd sauerbraten/src
    make clean
    make
    make install

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


# Applying the patch

The patch contains changes in data/ and src/fpsgame/

    cd sauerbraten
    patch -p1 < handicap_mod.diff
