---
layout: default
title: thumbsup setup
---

### Setup

There are 2 main ways to run `thumbsup`: straight up as an `npm` package, or using the pre-built Docker image.
They each have pros and cons, which one you choose depends on your requirements.

<table class="comparison">
  <tr>
    <th>npm</th>
    <th>docker</th>
  </tr>
  <tr>
    <td class="category" colspan="2">Dependencies</td>
  </tr>
  <tr>
    <td>Need to install manually (e.g. <code>ffmpeg</code>)</td>
    <td>All bundled in</td>
  </tr>
  <tr>
    <td class="category" colspan="2">Codecs</td>
  </tr>
  <tr>
    <td>Need to provide your own. Useful if you have specific video formats to process.</td>
    <td>Most common codecs built-in. You can create a derived image if you want to include new ones.</td>
  </tr>
  <tr>
    <td class="category" colspan="2">Performance</td>
  </tr>
  <tr>
    <td>As fast as your computer</td>
    <td>Up to 50% slower than the <code>npm</code> version.</td>
  </tr>
</table>

### As an npm package

**Requirements**

- [Node.js](http://nodejs.org/): `brew install Node`
- [GraphicsMagick](http://www.graphicsmagick.org/): `brew install graphicsmagick`
- [FFmpeg](http://www.ffmpeg.org/): `brew install ffmpeg`

*Note: there currently is [an issue with Ubuntu 14.04](#27) if you build `ffmpeg` from source. Please upgrade to 14.10 and install it with `apt-get`.*

**Installation**

```bash
npm install -g thumbsup
```

**Creating a basic gallery**

```bash
thumbsup --input ~/photos --output ~/gallery
```

For more details about all the arguments and options available, see the [configuration](/docs/configuration) page.

### As a docker container

**Requirements**

- [Docker](https://www.docker.com/products/docker)

**Installation**

```bash
docker pull thumbsup/thumbsup
```

**Creating a basic gallery**

```bash
docker run -t              \
  -v `pwd`:/work           \
  -u $(id -u):$(id -g)     \
  asyncadventures/thumbsup \
  thumbsup --input /work/media --output /work/gallery
```

You can of course mount the volumes differently.
The only requirement is to make sure the paths referenced are accessible from within the Docker container.

*Notes:*

- the `-t` argument is for the progress bars to render properly
- the `-u` argument is to avoid permission issues, where the generated gallery is owned by an unknown user

Photo dates displayed on the website are based on the current machine timezone.
When running in Docker, this is `GMT`. If the timezone is important to you, you should also add

```bash
docker run -v /etc/localtime:/etc/localtime [...]
```

For more details about all the arguments and options available, see the [configuration](/docs/configuration) page.

### Input folder structure

Any folder with photos and videos!
Using the default configuration, each folder will become an album.

```
input
  |__ paris
  |    |__ day 1
  |    |   |__ img001.jpg
  |    |   |__ img002.jpg
  |    |__ day 2
  |        |__ img003.jpg
  |        |__ img004.jpg
  |__ tokyo
       |__ img005.png
       |__ vid001.mp4
```

### Expected output

If the gallery generation works, you should expect an output similar to this:

```
$ thumbsup [args]

  List all files      [===================] 6/6 files
  Update metadata     [===================] 6/6 files
  Original photos     [===================] 6/6 files
  Original videos     [===================] 6/6 files
  Photos (large)      [===================] 5/5 files
  Photos (thumbs)     [===================] 5/5 files
  Videos (resized)    [===================] 1/1 files
  Videos (poster)     [===================] 1/1 files
  Videos (thumbs)     [===================] 1/1 files
  Static website      [===================] done

  Gallery generated successfully
```
