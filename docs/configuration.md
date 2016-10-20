---
layout: default
title: thumbsup configuration
---

### Configuration

The following arguments are required:

- `--input <path>` path to the folder with photos / videos
- `--output <path>` target output folder

And you can optionally specify:

- `--title [text]` website title (default: `Photo gallery`)
- `--thumb-size [pixels]` thumbnail image size (default: `120`)
- `--large-size [pixels]` fullscreen image size (default: `1000`)
- `--original-photos [true|false]` to allow download of full-size photos (default: `false`)
- `--original-videos [true|false]` to allow download of full-size videos (default: `false`)
- `--sort-albums [name|date]` how to sort the albums (default: `date`)
- `--theme [name]` name of the gallery theme to apply (default: `default`)
- `--css [file]` CSS or LESS styles to be applied on top of the theme (no default)
- `--google-analytics [code]` code for Google Analytics tracking (no default)

For example:

```bash
thumbsup --input "/media/photos" --output "./website" --title "My holidays" \
         --thumb-size 200 --large-size 1500 \
         --original-photos true --original-videos false \
         --sort-albums date  --theme default --css "./custom.css" \
         --google-analytics "UA-999999-9"
```

**Important notes**

- all paths are relative to the current working directory
- when `original` settings are off, the download link points to a web-friendly size
- when `original` settings are on, all original media is copied to the output folder

### JSON configuration

Maintaining many arguments can become tedious.
You might also want to save them somewhere and re-use them easily.
To help with this `thumbsup` also supports passing arguments as a `JSON` file:

```bash
thumbsup --config config.json
```

Simply specify all arguments as an object, without the `--` prefix:

```json
{
  "input": "/media/output",
  "output": "./website",
  "title": "My holiday",
  "thumb-size": 200,
  "large-size": 1500,
  "original-photos": true,
  "original-videos": false,
  "sort-albums": "date",
  "theme": "default",
  "css": "./custom.css",
  "google-analytics": "UA-999999-9"
}
```
