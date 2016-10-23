---
layout: default
title: Configuration
---

## Configuration

All `thumbsup` configuration is done passing command-line arguments.

### Command line arguments

The following arguments are required:

```bash
--input <path>    # path to the folder with photos / videos
--output <path>   # target output folder
```

And you can optionally specify:

```bash
--title [text]                  # website title (default: Photo gallery)
--thumb-size [pixels]           # thumbnail image size (default: 120)
--large-size [pixels]           # fullscreen image size (default: 1000)
--original-photos [true|false]  # include full-size photos for download (default: false)
--original-videos [true|false]  # include full-size videos for download (default: false)
--albums-from [folders|date]    # how files are grouped into albums (default: folders)
--albums-date-format [pattern]  # how albums are named in "date" mode (default: YYYY-MM)
--sort-albums [name|date]       # how to sort the albums (default: date)
--sort-media [name|date]        # how to sort files inside an album (default: date)
--theme [name]                  # name of the gallery theme to apply (default: default)
--css [file]                    # CSS/LESS file to apply on top of the theme (no default)
--google-analytics [code]       # code for Google Analytics tracking (no default)
```

For example it can be as simple as

```bash
thumbsup --input "/media/photos" --output "./website"
```
{: .single-line}

or as complex as

```bash
thumbsup --input "/media/photos" --output "./website" --title "My holidays" --thumb-size 200 --large-size 1500 --original-photos true --original-videos false --sort-albums date --theme default --css "./custom.css" --google-analytics "UA-999999-9"
```
{: .single-line}

All relative paths are relative to the current working directory.

### More details

#### \-\-original-photos / \-\-original-videos

When these settings are on, original files are copied into the output folder,
and a link is provided for download. When the settings are off, the download link
points to a web-friendly (resized) version instead.

#### \-\-albums-from

If you choose `folders`, the album structure will exactly mirror the folder structure on disk.
If you choose `date`, files will be grouped into albums based on their date - regardless of where they are on disk.

#### \-\-albums-date-format

This is only relevant if you chose `--album-from date`, and determines how albums are named.
It can be any valid [moment.js](http://momentjs.com/) date format. The format can contain
the `/` character to create nested albums. Some valid examples are:

- `YYYY MMMM` for a top-level `2016 October` album
- `YYYY/MM` for a top-level `2016` album, with a nested album called `10`
- `YYYY/YYYY MMMM` for a top-level `2016` album, with a nested album called `2016 October`

<div class="warning">
The date of a file is always the date is was taken, if available in the <code>EXIF</code> data.
If there is no EXIF data, it defaults to the file's <code>mtime</code>,
which you can change with many tools - including Unix's <code>touch</code> command.
</div>

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

<br />

<div style="margin: 2em 0; text-align: center;">
  <a class="btn btn-cta-primary" href="/docs/themes">Next: themes</a>
</div>
