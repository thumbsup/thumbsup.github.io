---
layout: default
title: Themes
---

## Themes

You can select a theme for the generated gallery with `--theme <name>`.
Themes don't impact the way thumbnails are generated, and simply change the final layout of the galleries.

To submit a theme, please [raise an issue on Github here](https://github.com/thumbsup/thumbsup).

### mosaic

In this theme, each album is represented as a strip of small thumbnails.

<div class="row theme-gallery">
  <div class="item col-md-6 col-sm-6 col-xs-12">
      <img src="/public/images/theme-mosaic-albums.png" alt="List of albums">
  </div>
  <div class="item col-md-6 col-sm-6 col-xs-12">
    <img src="/public/images/theme-mosaic-media.png" alt="Photos and videos">
  </div>
</div>

<div class="btns">
  <a class="btn btn-cta-secondary" href="/demos/themes/mosaic">See demo</a>
</div>

### cards

This theme uses a larger layout, with one large image per album.

<div class="row theme-gallery">
  <div class="item col-md-6 col-sm-6 col-xs-12">
      <img src="/public/images/theme-cards-albums.png" alt="List of albums">
  </div>
  <div class="item col-md-6 col-sm-6 col-xs-12">
    <img src="/public/images/theme-cards-media.png" alt="Photos and videos">
  </div>
</div>

<div class="btns">
  <a class="btn btn-cta-secondary" href="/demos/themes/cards">See demo</a>
</div>

### classic

This is theme was the default layout of `thumbsup` v1.
Each album is represented as a 2x2 square of previews.

<div class="row theme-gallery">
  <div class="item col-md-6 col-sm-6 col-xs-12">
      <img src="/public/images/theme-classic-albums.png" alt="List of albums">
  </div>
  <div class="item col-md-6 col-sm-6 col-xs-12">
    <img src="/public/images/theme-classic-media.png" alt="Photos and videos">
  </div>
</div>

<div class="btns">
  <a class="btn btn-cta-secondary" href="/demos/themes/classic">See demo</a>
</div>

<div style="margin-bottom: 3em;"></div>

## Customizing a theme

You can customise the look of a gallery by using `--css <file>`.
Your stylesheet will be rendered at the end of the site's `<head>`,
which means you can override any part of theme you want.
Just make sure the rules are specific enough to take effect. For example:

```bash
thumbsup --theme default --css custom.less
```

```css
// custom.less
.albums li {
  box-shadow: 1px 2px rgba(0, 0, 0, 0.3);
}
```

The file can be any valid CSS or LESS. Note you don't need to copy the file to the output folder,
as it's automatically concatenated with the rest of the theme.

<div style="margin: 2em 0; text-align: center;">
  <a class="btn btn-cta-primary" href="/docs/deployment">Next: deployment</a>
</div>
