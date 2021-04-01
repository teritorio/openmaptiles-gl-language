# OpenMapTiles Language

Adds support for switching the language of your map style in [Mapbox GL JS](https://www.mapbox.com/mapbox-gl-js/) maps.

**Requires [mapbox-gl-js](https://github.com/mapbox/mapbox-gl-js).** For other platforms, such as Android and iOS, see [this help document](https://www.mapbox.com/help/change-language/).

![Multiple language supported with style transforms](https://cloud.githubusercontent.com/assets/1288339/26266912/89b1b6ba-3cb5-11e7-9964-49f51290d627.gif)

_Automatic style transformations for different languages_

![Switch language based on user agent](https://cloud.githubusercontent.com/assets/1288339/26269878/742cdb02-3cc5-11e7-8479-c6ab3f0f8a82.gif)

_Switch language based on user agent_

**Example**

```javascript
var map = new mapboxgl.Map({
    container: 'map',
    style: 'mapbox://styles/mapbox/streets-v10',
    center: [-77.0259, 38.9010],
    zoom: 9
});

// Add RTL support if you want to support Arabic
// mapboxgl.setRTLTextPlugin('https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-rtl-text/v0.10.1/mapbox-gl-rtl-text.js');

var language = new OpenMapTilesLanguage();
map.addControl(language);
```

Check `examples/` for more usage examples.

## API

<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

#### Table of Contents

-   [OpenMapTilesLanguage](#OpenMapTilesLanguage)
    -   [Parameters](#parameters)
    -   [setLanguage](#setlanguage)
        -   [Parameters](#parameters-1)

### OpenMapTilesLanguage

Create a new [Mapbox GL JS plugin](https://www.mapbox.com/blog/build-mapbox-gl-js-plugins/) that
modifies the layers of the map style to use the `text-field` that matches the browser language.

As of Mapbox GL Language v1.0.0, this plugin no longer supports token values (e.g. `{name}`). v1.0+ expects the `text-field`
property of a style to use an [expression](https://docs.mapbox.com/mapbox-gl-js/style-spec/expressions/) of the form `['get', 'name_en']` or `['get', 'name']`; these expressions can be nested. Note that `get` expressions used as inputs to other expressions may not be handled by this plugin. For example:
```
["match", 
  ["get", "name"], 
  "California", 
  "Golden State", 
  ["coalesce", 
    ["get", "name_en"], 
    ["get", "name"]
  ]
]
```
Only styles based on [OpenMapTiles styles](https://openmaptiles.org/) are supported.

#### Parameters

-   `options` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Options to configure the plugin.
    -   `options.supportedLanguages` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)>?** List of supported languages
    -   `options.languageTransform` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** Custom style transformation to apply
    -   `options.languageField` **[RegExp](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/RegExp)** RegExp to match if a text-field is a language field (optional, default `/^name_/`). Note that as of Mapbox GL Language v1.0.0, token values (e.g. `{name}`) are no longer supported.
    -   `options.getLanguageField` **[Function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function)?** Given a language choose the field in the vector tiles
    -   `options.languageSource` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Name of the source that contains the different languages.
    -   `options.defaultLanguage` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)?** Name of the default language to initialize style after loading.
    -   `options.excludedLayerIds` **[Array](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array)&lt;[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)>?** Name of the layers that should be excluded from translation.

#### setLanguage

Explicitly change the language for a style.

##### Parameters

-   `style` **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** Mapbox GL style to modify
-   `language` **[string](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String)** The language iso code

Returns **[object](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object)** the modified style

## Develop

Run the linter and watch for changes to rebuild with browserify.

    npm install
    npm run test

## Languages

Showcasing the languages supported by OpenMapTiles.

-   [Your Browser language](https://mapbox.github.io/mapbox-gl-language/examples/browser.html)
-   [Arabic](https://mapbox.github.io/mapbox-gl-language/examples/ar.html)
-   [Chinese Simplified](https://mapbox.github.io/mapbox-gl-language/examples/zh.html)
-   [English](https://mapbox.github.io/mapbox-gl-language/examples/en.html)
-   [French](https://mapbox.github.io/mapbox-gl-language/examples/fr.html)
-   [German](https://mapbox.github.io/mapbox-gl-language/examples/de.html)
-   [Italian](https://mapbox.github.io/mapbox-gl-language/examples/it.html)
-   [Japanese](https://mapbox.github.io/mapbox-gl-language/examples/ja.html)
-   [Korean](https://mapbox.github.io/mapbox-gl-language/examples/ko.html)
-   [Multilingual](https://mapbox.github.io/mapbox-gl-language/examples/multilingual.html)
-   [Portuguese](https://mapbox.github.io/mapbox-gl-language/examples/pt.html)
-   [Russian](https://mapbox.github.io/mapbox-gl-language/examples/ru.html)
-   [Spanish](https://mapbox.github.io/mapbox-gl-language/examples/es.html)

## Supported Styles

You can configure the plugin to support your own custom style using style transforms and custom language fields.
By default, this plugin works best with [OpenMapTiles styles](https://openmaptiles.org/styles/) or derived.
