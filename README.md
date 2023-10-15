# LinuxGSG
GSG Is a game script  generator. Allows you to automatically create sh files to run games.

The purpose is to allow users to run games just with Wine and winetricks packages, no proton, lutris or whatever in a straightfoward way, and also generate
scripts that will allow users to launch games on emulators immediatly with the needed arguments.

this does NOT configure automatically the emulators, you have to do that on your own.

# Contributing

If a game setup that you know is missing in the `game setups.txt` file inside `PC` folder, please create an issue with the appropriate labels.
I will add the wine configuration and if available, the necessary DLL overrides in the script for the missing game.

if in the script there is a missing game that contains the main .exe in a subfolder, please report it and i will add it to the
local comparison in the script.


# Currently Supported extension detection:
```
PC (.exe)

PCSX2 (.iso)

mGBA (.gbc | .gba | .gb)

Xemu (.iso)

Xenia (.xex | .iso | .zar)

MelonDS (.nds | .dsi | .ids | .app)

Citra (.cia | .3ds)

PPSSPP (.iso)

Duckstation (.bin | .iso | .img)  

Yuzu/Ryujinx (.xci | .nsp)
```
# Depencies
winetricks for wine packages, Zenity or Dialog for UI. (recommended zenity for now)

# Initial Setup
- First of all, setup your games by following the Game Setups txt document. If a game is not available please report it
  and if possible, add documentation about what it needs to run in wine via github issues.
- Games must be in their individual folders, regrouped in a subfolder.
- if more than one `.exe` file is in the same dir, rename the non necessary ones into `.EXE` or remove the extension. the wine parser
  parses recursively for *.exe files.

# How to use

I provided a UI with Zenity (dialog support coming soon)
All you have to do is configure the requested paths.

This will generate a `start.sh` in each game folder to allow you to run the games with a single execution instead of manually
searching for the file, write the commands and run it, it also applies arguments if known.

You can tweak the wine parser to add more specific game cases for the script generation.
only the WINE parser can beed tweaks based on your game folder names with the comparisons.

# Integrating with steam rom manager

We can run these generated scripts from steam with steam rom manager. To do so you have to create a parser with these settings:

```
Parser type: glob

Config title: put name here

Steam directory: usually /home/user/.steam/root

User Accounts: ${Steam Username}

Steam category: Category name

ROMs directory: /path/to/your/games

Executable: /usr/bin/bash

command line arguments: "${filePath}"

User's glob: ${title}/start.sh

For portaits it is recommended to use a 500x700 image with an extension you want, each cover must be put in the main game folder
not in subfolders.

Local portraits image: /path/to/games/${title}/*@(.jpg)
```

Run the parser and it will detect all the "start.sh" created for each game folder in the specified path, and it will associate the covers we made.

You can duplicate this parser and change the category, title name and ROM's path since now everything uses a `sh` file as a base to run the games, emulators ecc,

You won't have to make specific configurations for each executable, the arguments are also included in the generated sh files.


# Special Thanks

SSUPII - Dialog Implementation https://github.com/SSUPII
