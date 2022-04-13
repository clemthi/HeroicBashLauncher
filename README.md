<img alt="GitHub" src="https://img.shields.io/github/license/redromnon/HeroicBashLauncher?style=for-the-badge">   <img alt="GitHub release (latest by date including pre-releases)" src="https://img.shields.io/github/v/release/redromnon/HeroicBashLauncher?color=blue&include_prereleases&style=for-the-badge">    <img alt="GitHub Repo stars" src="https://img.shields.io/github/stars/redromnon/HeroicBashLauncher?color=yellow&style=for-the-badge">  <img alt="GitHub closed issues" src="https://img.shields.io/github/issues-closed/redromnon/HeroicBashLauncher?color=blueviolet&style=for-the-badge">  <img alt="GitHub top language" src="https://img.shields.io/github/languages/top/redromnon/HeroicBashLauncher?color=green&style=for-the-badge">  <img alt="GitHub all releases" src="https://img.shields.io/github/downloads/redromnon/HeroicBashLauncher/total?color=red&style=for-the-badge">

# HeroicBashLauncher

Ever wanted to launch your Epic Games Store and GOG games installed through [Heroic Games Launcher](https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher) directly from the terminal, Lutris, Steam or any other frontend game launcher? 
Heroic Bash Launcher lets you do this very easily. 

You can now launch your game directly without having to open Heroic at all. There's no need to run `heroic` to find the game's launch command or write your own launch script with [Legendary](https://github.com/derrod/legendary)! Thus saving your time!


![Heroic Bash Launcher](https://user-images.githubusercontent.com/74495920/142615495-a4e5e811-7ee3-41b8-ae80-d6d008820f2a.png)


## Pre-requisites
- Heroic 2.2.2+
- Zenity

## Building & Testing
Since the program makes use of an executable, you will need **Python version 3.8+ and PyInstaller** to build the code.

You will also need [wget (for Python)](https://pypi.org/project/wget/).

To test the program, open the terminal in the `func` directory and use the following command to build -

```
pyinstaller HeroicBashLauncher.py --onefile -p <fullpath>/HeroicBashLauncher/func
```

This will generate an executable stored in the `dist` folder. Copy the executable, paste it in `HeroicBashLauncher` and run it.

## Installation
Head over to the [Releases](https://github.com/redromnon/HeroicBashLauncher/releases) page. Then download and extract the **.zip** file of the latest release.

## Usage

### Running the Program
Execute the program by simply running the `setup.sh` script. You should be greeted by the _Process Finished_ dialog at the end.


### Running Games
You can run your game by executing the game's launch script by double-clicking the game's launch scipt, using the terminal like ```./RocketLeague_Heroic.sh``` or using your preferred game launcher/manager just point the executable path to the game's launch script. Simple!

**Don't copy or move the game files and launch scripts anywhere else, it won't work.** 

### Handy Guides

- [Steam Deck extended guide](https://github.com/redromnon/HeroicBashLauncher/wiki/Steam-Deck-(Flatpak)-Guide)
- [Adding Heroic games to Lutris and GameHub](https://github.com/redromnon/HeroicBashLauncher/wiki/Adding-Games-to-Game-Launchers-&-Managers)
- [Syncing games to Steam](https://github.com/Heroic-Games-Launcher/HeroicGamesLauncher/wiki/Adding-Games-to-Steam-on-Linux#adding-your-games-to-steam)


## Working

Heroic Bash Launcher automatically detects installed games and creates a launch script for each game. It basically reads the `.json` files stored in `~/.config/heroic/GamesConfig`. 

The launch script is created using the *bash shell script*, i.e. `.sh` files. For example, if I have Rocket League installed, it will create the launch script titled "RocketLeague.sh". All these launch scripts will be available in the **GameFiles** folder. 

Every game's launch script will contain all the launch parameters according to the game's setting in Heroic Games Launcher, including cloud syncing for supported games. 

The program also automatically downloads and adds the cover art when the launch scripts are added to Steam ( See **Syncing games to Steam** above )

Here's an example below of _"RocketLeague_Heroic.sh"_ -

```
#!/bin/bash 

#Generate log
exec > logs/RocketLeague_Heroic.log 2>&1

#Game Name = Rocket League (EPIC) 

#App Name = Sugar

#Overrides launch parameters
cd .. && ./HeroicBashLauncher "Rocket League" "Sugar" "/home/redromnon/.config/heroic/GamesConfig/Sugar.json" "epic" 



(WINE_FULLSCREEN_FSR=1 WINE_FULLSCREEN_FSR_STRENGTH=2 WINEESYNC=1 mangohud --dlsym /opt/Heroic/resources/app.asar.unpacked/build/bin/linux/legendary launch Sugar --wine '/home/redromnon/.config/heroic/tools/wine/Wine-7.2-GE-2/bin/wine' --wine-prefix '/home/redromnon/.wine' || (echo "---CANNOT CONNECT TO NETWORK. RUNNING IN OFFLINE MODE---" ; WINE_FULLSCREEN_FSR=1 WINE_FULLSCREEN_FSR_STRENGTH=2 WINEESYNC=1 mangohud --dlsym /opt/Heroic/resources/app.asar.unpacked/build/bin/linux/legendary launch Sugar --offline --wine '/home/redromnon/.config/heroic/tools/wine/Wine-7.2-GE-2/bin/wine' --wine-prefix '/home/redromnon/.wine' )) || (zenity --error --title="Error" --text="Failed to launch games 

Consider posting the log as an issue" --width=200 --timeout=3)

```


## Features Planned

- Ask user for a default path for saving game launch scripts
- Additional game launch options support (Eg. ARK)
- GUI


## Issues and Suggestions
If the program doesn't produce the game bash files (launch scripts), update the launch parameters, launch the games or displays an error dialog, consider checking the logs. The logs for the game launch scripts and the program are present in `/GameFiles/logs`and the base directory respectively.

Feel free to suggest any new features, especially those already implemented in Heroic. 

## License
This project is under the GNU GPLv3 license. You can take a look at the LICENSE.md for more information.


## You can check out the Wiki for [FAQs](https://github.com/redromnon/HeroicBashLauncher/wiki/FAQ) and [Changelog](https://github.com/redromnon/HeroicBashLauncher/wiki/Changelog)
