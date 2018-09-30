# RPG Maker MV Game Player
This is the game engine for RPG Maker MV. By default, the core scripts are merged and creates a long js file. This repository exists for plugin developers to have an easy time to reference the code and find the changes of the engine. This repository will be updated when the engine does.

## rpg_core.js
Features base classes such as audio and input processing. It also contains the wrapper classes from Pixi.js

## rpg_managers.js
Static classes named XxxManager that manage the game overall.

## rpg_objects.js
Classes named Game_Xxx dealing with game data (many are saved).

## rpg_scenes.js
Classes named Scene_Xxx in which the scene is defined.

## rpg_sprites.js
Classes named Sprite_Xxx related to image display and processing.

## rpg_windows.js
Classes named Window_Xxx handling window display and input.

## Extra
In addition, a plugin list is defined in plugins.js, and main.js launches the game.
