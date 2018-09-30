# RPG Maker MV Game Player
This is the game engine for RPG Maker MV. By default, the core scripts are merged and creates a long js file. This repository exists for plugin developers to have an easy time to reference the code and find the changes of the engine. This repository will be updated when the engine does. If you want to know how to work with the corescripts, refer to [Corescript Collaboration](https://github.com/rpgtkoolmv/corescript)

## Constitution
The core script is finally output to mainly 6 files.
<dl>
    <dt>rpg_core.js</dt>
    <dd>Features base classes such as audio and input processing. It also contains the wrapper classes from Pixi.js</dd>
    <dt>rpg_managers.js</dt>
    <dd>Static classes named XxxManager that manage the game overall.</dd>
    <dt>rpg_objects.js</dt>
    <dd>Classes named Game_Xxx dealing with game data (many are saved).</dd>
    <dt>rpg_scenes.js</dt>
    <dd>Classes named Scene_Xxx in which the scene is defined.</dd>
    <dt>rpg_sprites.js</dt>
    <dd>Classes named Sprite_Xxx related to image display and processing.</dd>
    <dt>rpg_windows.js</dt>
    <dd>Classes named Window_Xxx handling window display and input.</dd>
    <dt>Others</dt>
    <dd>In addition, a plugin list is defined in plugins.js, and main.js launches the game.</dd>
</dl>

