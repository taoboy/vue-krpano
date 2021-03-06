![Somewhats](http://is2.mzstatic.com/image/thumb/Purple127/v4/36/ec/67/36ec677d-1556-8811-9b02-3b3931657f01/source/175x175bb.jpg)

# vue-krpano

A Vue component for [krpano](http://www.krpano.com) player.

## Demo

[https://www.somewhats.cn/pois/10045](https://www.somewhats.cn/pois/10045)

[https://itunes.apple.com/cn/app/%E5%A3%B9%E4%BA%8C/id1190188895?l=en&mt=8](https://itunes.apple.com/cn/app/%E5%A3%B9%E4%BA%8C/id1190188895?l=en&mt=8)

## Installation

```
npm install vue-krpano --save
```

## Dependency

* [vuejs@2.0](http://vuejs.org)
* A Krpano player globally referenced by `<script>`


## Example

Install the component

```js

import Vue from "vue";
import Krpano from "vue-krpano";


Vue.use(Krpano);

```

Use the component

```html
<krpano :xml="'krpano.xml'" :lazy-load="true" style="width:100%;height:400px" @panoCreated="init"></krpano>
```

## Props

|Name|Description|Example|
|:--|:--|:--|
|`xml`|Krpano configuration XML path|`krpano.xml`|
|`scene`|Scene name|`foo`|
|`lazyLoad`|A Boolean setting to lazy load pano objects|`true`|
|`freezeVertical`|A Boolean setting to freeze scrolling vertically|`false`|
|`hooks`|An object that will be attached to the `krpano` instance|`{foo:bar}`|
|`debug`|Debug mode|`false`|

### Krpano builtin options

|Name|Description|Example|
|:--|:--|:--|
|`bgcolor`|The background color of the viewer (in html color format).|`#000000`|
|`wmode`|The wmode setting is typically a Flashplayer setting, but wmode=opaque and wmode=transparent<br/> will be evaluated also by the krpano HTML5 viewer and make the viewer background transparent there too. <br/>Overlapping html elements itself are always possible when using the HTML5 viewer.|`opaque`|
|`vars`|Pass a Javascript Object with krpano variable:value pairs.<br/>The variables will be set AFTER the xml file has been be loaded and parsed.<br/>So these variables can be used to add new settings or to overwrite settings that were already defined in the xml.||
|`initvars`|Pass a Javascript Object with krpano variable:value pairs.<br/>This is basically the same as the vars setting, <br/>but these variables will be set BEFORE the xml file wil be loaded and parsed.||
|`basepath`|Can be used in Flash and HTML5 for adjusting relative paths in the xml.||
|`mwheel`|A Boolean setting to control the mouse-wheel usage|`false`|
|`focus`|A Boolean setting to give the viewer the input / keyboard focus on startup.|`true`|
|`consolelog`|A Boolean setting that defines if krpano log/trace-messages should be sent also to the browser Javascript console.|`false`|
|`webglsettings`|Pass an object with special settings for the WebGL context creation.<br/>The WebGL context will be created at startup and can't be changed at runtime, therefore these settings need to be specified already during embedding.||
|`mobilescale`|By default all krpano content on mobile devices will be scaled by 0.5.<br/>To disable that scaling, set the mobilescale setting to 1.0.<br/>This can be useful for implementing responsive webdesigns.|`0.5`|
|`fakedevice`|Fake the krpano device detection settings.<br/>Available settings: `mobile`, `tablet`, `desktop`.|`mobile`|

## Events

### panoCreated

This event will be fired along with a krpano object as soon as the krpano instance is successfully initialized.

### sceneChanged

This event will be fired every time the scene is changed. The scene name will also be involved.


## Two-way Communication

The `hooks` object will be attached to the `krpano` instance.

Example:

The Vue component wants to capture the event when user click the route spot in pano scenes.

```vue
<script>
    export default {
        data(){
            const vm = this;
            return {
                xml: "xml path",
                scene: "scene name",
                hooks:{
                    sceneChanged(scene){
                        //event handler
                    }
                }                
            }
        }
    }
</script>
<template>
    <krpano :xml="xml" :scene="scene" :hooks="hooks"></krpano>
</template>
```

In krpano scripts, you can access the callback object via [krpano](https://krpano.com/docu/actions/#jscall
) instance.

```xml
<events name="player_listener" keep="true" onnewscene="on_scene_loaded()"/>
<action name="on_scene_loaded">
    jscall(calc('krpano.hooks.sceneChanged("' + scene[get(xml.scene)].name + '")'));
</action>
```

## About

For any question, please feel free to write email to chshapple@gmail.com

