# OpenPrefirePrac (WIP)

An open-source CounterStrikeSharp powered server-side practicing plugin for CS2. It provides multiple prefire practices on competitive map pool maps and support multiplayer practicing concurrently.

## How to use

### Requirement

- CounterStrikeSharp v178

### Installation

Currently I only provide the Linux (amd64) version. Download [the latest release files](https://github.com/lengran/OpenPrefirePrac/releases) and extract all files into **game/csgo/addons/counterstrikesharp/plugins/OpenPrefirePrac/**.

To install the latest version of CounterStrikeSharp, please refer to this [guide](https://docs.cssharp.dev/docs/guides/getting-started.html).

### Tips on operating a practice server

When starting a server, I recommend using these parameters.

```bash
[CS2 Installation Directory]/game/bin/linuxsteamrt64/cs2 -dedicated -insecure +map de_inferno -maxplayers_override 64 +game_alias competitive
```

Note: "-maxplayers_override 64" is the most important one. It allows the server to add more than 5 bots on one team, which is crucial to achieve the goal of allowing multiplayer training simultaneously.

## How to create a practice profile?

The folder "map" is organize as follows. Each sub-folder in "map" contains practice profiles for the corresponding map. Each text file in that sub-folder is a practice profile.

A practice profile consists of 3 parts.

The first line contains the name of incompatible practices, separated by spaces.

The second line indicates how many bots are needed in this practice.

The third line instructs the place and facing direction of the player. The first 3 floating numbers are the position and the other 3 are the rotation.

```
pos_x pos_y pos_z ang_x ang_y ang_z
```

The fourth part with an arbitrary number of lines describes how to place bots. The first 3 numbers is position, following 3 numbers of the rotation. The 7th value is either True of False indicating whether the bot is crouching.

```
pos_x pos_y pos_z ang_x ang_y ang_z is_crouching
```

The positions and facing rotations can be retrived from in-game get\_pos command. But please notice that, the height values used in profiles should be the values returned by get\_pos minus 65. I made a python script that does this calculation for you. You can stack the strings retured by get\_pos and put them in a txt file, and pass the file to the python script as described below and the script will automatically print out the formatted bot positions.

```bash
python3 calculate_height.py [PATH TO YOUR FILE]
```

The fifth part with an arbitrary number of lines describes joint points of a guiding line. The guiding line is used to provide a better narration of how the practice is designed to be played.

```
pos_x pos_y pos_z
```

This can also be extracted from get\_pos using the python script. It will read in lines composed of 4 parts (e.g. "setpos 1348.844727 -989.403198 -103.968750") and calculate the height values for you.

```bash
python3 calculate_height.py [PATH TO YOUR FILE]
```

## Current development progress

Current it's still under active developing.

Finished practices:

- de_inferno
    - A short to A site
    - A long to A site
    - A apartments to A site
    - Banana to B site
    - Retake B from CT spawn
- de_ancient
    - B ramp to B site
    - B house to B site
    - Mid to A site
    - A main to A site
    - Retake A from CT spawn
- de_mirage
    - Attack A site from A ramp (to CT spawn)
    - Attack B site from B apartments
    - Attack A site from A palace (to jungle)
- de_dust2
    - Attach A site from A long
    - Attach A site from A short

TODO:

1. Create prefire profiles for all maps.
2. Draw guiding lines on the floor.
3. Improve bot logic.
4. Improve localization support (The supporting framework is done. Submitting translations is warmly welcomed.).
5. Reroute saperate logs into one gathered place for better debug experience.

## Reference

I have referred these open-source projects during the development.

- https://github.com/shobhit-pathak/MatchZy/
- https://github.com/B3none/cs2-retakes
- https://github.com/aprox2/GeoLocationLanguageManagerPlugin
- https://github.com/daffyyyy/CS2-SimpleAdmin

This project is inspired by a close-source prefire plugin developed by https://space.bilibili.com/283758782.

Huge thanks.