grunt-webp
==========

Convert your images to [WebP](https://developers.google.com/speed/webp/) format. This is a fork of [somerandomdude/grunt-webp](https://github.com/somerandomdude/grunt-webp), but with both backwards compatible and incompatible changes. 

![Console output](http://i.giphy.com/l0HlJGqrjflJRQO9W.gif "Description goes here")

## Getting Started

To install this plugin, open up the terminal, `cd` to your project's root directory and run the following command:

```shell
npm install ayesh/grunt-webp --save-dev
```

This plugin depends on WebP's `cwebp` encoder. You'll need to install the [WebP Package](https://developers.google.com/speed/webp/download) or use [webp-bin](https://github.com/yuanyan/node-webp-bin)

In your `Gruntfile.js` file add the following line:

```js
grunt.loadNpmTasks('grunt-webp');
```

This plugin requires Grunt `~0.4.0`

### Settings 

* __binpath (string)__ Location of the cwebp executable, default 'cwebp'. Use forward slashes as directory separator.
* __quality (float)__ Quality factor (0:small..100:big).
* __alphaQuality (integer)__ Transparency-compression quality (0..100)
* __preset (string)__ Preset setting, one of: _default_, _photo_, _picture_, _drawing_, _icon_, _text_
* __compressionMethod (integer)__ Compression method (0=fast, 6=slowest). 
* __segments (integer)__ Number of segments to use (1..4). 
* __psnr (float)__ Target PSNR (in dB. typically: 42). 
* __sns (integer)__ Spatial Noise Shaping (0:off, 100:max). 
* __filterStrength (integer)__ filter strength (0=off..100). 
* __filterSharpness (integer)__ Filter sharpness (0:most .. 7:least sharp). 
* __simpleFilter (boolean)__ Use simple filter (default is false). 
* __partitionLimit (integer)__ Limit quality to fit the 512k limit on the first partition (0=no degradation ... 100=full). 
* __analysisPass (integer)__ Analysis pass number (1..10). 
* __crop (array)__ Crop picture with the given rectangle. [x, y, width, height]
* __resizeCrop (array)__ Resize picture (after any cropping). [width, height]
* __multiThreading (boolean)__ Use multi-threading if available. 
* __lowMemory (boolean)__ Reduce memory usage (slower encoding). 
* __alphaMethod (string)__ Transparency-compression method (0..1). 
* __alphaFilter (string)__ Predictive filtering for alpha plane. One of: _none_, _fast_ (default) or _best_. 
* __alphaCleanup (boolean)__ Clean RGB values in transparent area. 
* __noAlpha (boolean)__ Discard any transparency information. 
* __lossless (boolean)__  Encode image losslessly.

Additional settings introduced in this fork:

* __quite (boolean)__  Shuts up the webp program output. This results in a minimal output that you CI server would love.
* __deleteLarger (boolean)__  The most important change from this fork. Deletes the converted webp if it is larger than its source file.

## Example


```js
module.exports = function(grunt) {

  
  grunt.initConfig({
	// WebP configuration
    webp: {
      files: {
        expand: true,
        cwd: 'path/to/source/images',
        src: 'source/*.png',
        dest: 'output/path/'
      },
      options: {
        binpath: require('webp-bin').path, // Or, omit this configuration to use use cwebp from path. You can also put the absolute path to cwebp executable here.
        preset: 'photo',
        verbose: true,
        quality: 90, // We recommend quality 90.
        alphaQuality: 80,
        compressionMethod: 6,
        segments: 4,
        psnr: 42,
        sns: 50,
        filterStrength: 40,
        filterSharpness: 3,
        simpleFilter: true,
        partitionLimit: 50,
        analysisPass: 6,
        multiThreading: true,
        lowMemory: false,
        alphaMethod: 0,
        alphaFilter: 'best',
        alphaCleanup: true,
        noAlpha: false,
        lossless: false,
        quite: true,
        deleteLarger: true
      }
    }

  });

  // load npm task
  grunt.loadNpmTasks('grunt-webp');

  // register task
  grunt.registerTask('default', 'webp');

};
```

### Changes in this fork

 - The output is heavily modified. It now reports how much savings it made. 
 - Deletes the convereted file if it is larger. 
 - At the end of operation, a summary will be shown. 
