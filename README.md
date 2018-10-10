# RPG Maker MV Game Player
This is the game engine for RPG Maker MV. By default, the core scripts are merged and creates a long js file. This repository exists for plugin developers to have an easy time to reference the code and find the changes of the engine. This repository will be updated when the engine does. If you want to work with the core scripts, refer to [Core script Collaboration.](https://github.com/rpgtkoolmv/corescript)

## Documentation
<dl>
    <dt>Script Call List by Archeia and RMW</dt>
    <dd>https://docs.google.com/spreadsheets/d/1-Oa0cRGpjC8L5JO8vdMwOaYMKO75dtfKDOetnvh7OHs/edit#gid=0</dd>
    <dt>Library Documentation by Kino: </dt>
    <dd>https://kinoar.github.io/rmmv-doc-web/index.html</dd>
</dl>


## How to build

To build Corescripts, install Node.js, change working directory, and just type in console:

```
npm install
npm run build
```

Then you can find Corescripts in folder “dist”

If you want to build indivisually, Here’s some command,
```
npm run build:core
npm run build:managers
npm run build:objects
npm run build:scenes
npm run build:sprites
npm run build:windows
```

To test, place MV’s project in game/ and type

```
npm test
```

There are helpful tasks, watch and start.

Watch task is watching js/rpg_*** changes, concat them, and copy that to ./game/js/ .

```
npm run watch
```

Start task starts local server. You can test Corescripts in your browser.

http://localhost:8080/

```
npm start
```

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

## Inheritance style

```js
// In JavaScript this function is constructor
function Derived() {
    this.initialize.apply(this, arguments); // Delegate to initialize()
}

Derived.prototype = Object.create(Base.prototype); // Derived inherits from Base
Derived.prototype.constructor = Derived;

Derived.prototype.initialize = function () {
    Base.prototype.initialize.call(this); // This makes super.initialize() sense
};
```

## Global variables
Variables named `$dataXxx` are read from JSON in the *data* folder.
These files are changed by the editor, but they are immutable during play.
Variables named `$gameXxx` are instances of the class defined in *rpg_objects.js*.
When saving the game, these objects (except `$gameTemp, $gameMessage, $gameTroop`) are serialized to JSON and saved.
When loading, since the prototype chain is reconnected simultaneously with deserialization, you can continue using instance methods.

## Scene graph
The scene graph is a drawing tree like FLASH provided by Pixi.js.
Children are influenced by parent's coordinates and visibility.
Register a child in the form `(scene or sprite or window).addChild(child)`.

### Scene
In RMMV the scene is the root element of the scene graph and has children with Sprite and Window.
The life cycle is managed by `SceneManager`, and it operates up to one at the same time.

Life cycle: `new Scene_Xxx() -> create() -> start() -> update()* -> stop() -> terminate()`

## Flow

### Initialization
1. When the page is loaded, call `SceneManager.run()`. *(main.js)*
1. Initialize classes such as `Graphics, WebAudio, Input, TouchInput`.
1. Set `Scene_Boot` to `SceneManager`.
1. Register `SceneManager.update` in `requestAnimationFrame`.

`requestAnimationFrame` is called by the browser at regular time intervals (every time drawing is required).

### Update
1. `requestAnimationFrame` calls `SceneManager.update()`.
1. Process the current scene every 1/60 second according to the scene lifecycle rule
1. If `Scene_Xxx.update()` is called, then
    1. Call all children `update()`.
    1. Children recursively call their children `update()`.
1. Render the scene (including its children) onto the screen.
1. Register `SceneManager.update` in `requestAnimationFrame`.


## License
This content is released under the (http://opensource.org/licenses/MIT) MIT License.
