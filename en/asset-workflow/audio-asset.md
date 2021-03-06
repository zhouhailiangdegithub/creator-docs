# Audio asset

Audio resources are simple audio files.

Gmae engine plays different sound resources for game background music and sound effects through basic interface of various platforms.

## About the loading mode of sound

In the **Assets**, select an audio, the **Properties** will have a option of load mode. This option is only valid for the web platform.

### Web Audio

![web_audio.png](atlas/web_audio.png)

Loading audio resources with Web Audio, the audio resources will be cached in a buffer of the engine.

The advantage of this approach is good compatibility and robust. However the disadvantage is that too much memory will be occupied.

### DOM Audio

![dom_audio.png](atlas/dom_audio.png)

By generating a standard element to play the sound resources, the cache is the audio element.

When using standard audio elements to play sound resources, you may encounter some restrictions on some browsers. For example, each play must be played within the user action event (Web Audio only requires the first time), allowing only one sound resource to be played.

For larger Audio such as background music, DOM Audio is recommended.

### Dynamically select load mode

Sometimes we may not use the automatic loading or preload function of the scene, but we want to load it through `cc.loader` in our script.

#### default load mode

Audio is loaded and played by default using Web Audio, and DOM mode is used only in browsers that are not supported.

```js
cc.loader.load(cc.url.raw('resources/background.mp3'), callback);
```

#### Force use DOM mode to load

Audio in the loading process, will read the url get parameter. Which only need to define a useDom parameter.

```js
cc.loader.load(cc.url.raw('resources/background.mp3?useDom=1'), callback);
```

It should be noted that if you use the DOM mode to load the audio, in the cc.loader cache, the cache will also have the url? UseDom = 1. It is not recommended to fill in the url of the resource directly, try to define an AudioClip in the script, and then define it in the editor.

<hr>

Continue on to read about [Prefabricate Asset](prefab.md).