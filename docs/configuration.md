---
layout: default
title: Configuration
---

## Configuration

All `thumbsup` configuration is done passing command-line arguments.

### Command line arguments

The following arguments are required:

```bash
--input <path>   # Path to the folder with all photos/videos  [string] [required]
--output <path>  # Output path for the static website  [string] [required]
```

And you can optionally specify:

```bash
Output options:
  --thumb-size       # Pixel size of the square thumbnails  [number] [default: 120]
  --large-size       # Pixel height of the fullscreen photos  [number] [default: 1000]
  --original-photos  # Copy and allow download of full-size photos  [boolean] [default: false]
  --original-videos  # Copy and allow download of full-size videos  [boolean] [default: false]
  --cleanup          # Remove any output file that's no longer needed  [boolean] [default: false]

Album options:
  --albums-from            # How to group media into albums  [choices: "folders", "date"] [default: "folders"]
  --albums-date-format     # How albums are named in <date> mode [moment.js pattern]  [default: "YYYY-MM"]
  --sort-albums-by         # How to sort albums  [choices: "title", "start-date", "end-date"] [default: "start-date"]
  --sort-albums-direction  # Album sorting direction  [choices: "asc", "desc"] [default: "asc"]
  --sort-media-by          # How to sort photos and videos  [choices: "filename", "date"] [default: "date"]
  --sort-media-direction   # Media sorting direction  [choices: "asc", "desc"] [default: "asc"]

Website options:
  --index                 # Filename of the home page  [default: "index.html"]
  --albums-output-folder  # Output subfolder for HTML albums (default: website root)  [default: "."]
  --theme                 # Name of the gallery theme to apply  [choices: "classic", "cards", "mosaic"] [default: "classic"]
  --title                 # Website title  [default: "Photo album"]
  --footer                # Text or HTML footer  [default: null]
  --css                   # Path to a custom provided CSS/LESS file for styling  [string]
  --google-analytics      # Code for Google Analytics tracking  [string]
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

#### \-\-cleanup

When enabled (`--cleanup true`) this will generate the website as usual,
but also delete any **output** media files that are no longer referenced.

For example if you delete a photo from the **input** folder,
it will automatically delete the corresponding thumbnail since no album refers to it anymore.

*Note:* this never deletes any files from the input folder itself.

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

#### \-\-albums-output-folder

The default settings is for all HTML pages to sit at the root of the gallery.
This setting lets you group albums into a subfolder, so that the output looks like

```
output
  |__ index.html
  |__ albums
  |   |__ album-1.html
  |   |__ album-2.html
  |__ media
  |   |__ photo0001.jpg
  |   |__ photo0002.jpg
  |__ public
      |__ styles.css
```

This can help keep the output clean if you want to.
All relative links are still maintained for local browsing.

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
