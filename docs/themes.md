---
layout: default
title: Themes
---

## Themes

You can select a theme for the generated gallery with `--theme <name>`.
Here are the current themes available:

<div class="row theme-gallery">
  <!-- Default -->
  <div class="item col-md-4 col-sm-4 col-xs-12">
      <img src="/public/images/theme-default.jpg" alt="Default theme">
      <div class="theme-caption">
        Default <br />
        <a href="https://thumbsup.github.io/demos">See the demo site</a>
      </div>
  </div>
  <!-- Coming soon -->
  <div class="item col-md-4 col-sm-4 col-xs-12">
      <img src="/public/images/theme-coming-soon.jpg" alt="New theme">
      <div class="theme-caption">
        Coming soon... <br />&nbsp;
      </div>
  </div>
  <!-- Coming soon -->
  <div class="item col-md-4 col-sm-4 col-xs-12">
      <img src="/public/images/theme-coming-soon.jpg" alt="New theme">
      <div class="theme-caption">
        Coming soon... <br />&nbsp;
      </div>
  </div>
</div>

To submit a theme, please [raise an issue on Github here](https://github.com/thumbsup/node-thumbsup).

### Customizing a theme

There are two ways to customize the style of your galleries.
They both rely on the `--css` argument to pass an additional stylesheet.

```bash
thumbsup --theme default --css custom.less
```

Some themes have [LESS](http://lesscss.org/) variables that you can customize.
Simply provide a LESS file with your values, e.g.

```sass
// custom.less
@myvariable: #cef9b6;
```

The custom stylesheet is applied on top of the theme's base stylesheet.
This means you can actually override any style - just make sure they are specific enough to take effect.
For example:

```css
// custom.less
.albums li {
  box-shadow: 1px 2px rgba(0, 0, 0, 0.3);
}
```

### Theme variables

Here are all the [LESS](http://lesscss.org/) variables that can be overridden for a theme:

#### Default theme

```sass
@body-background: #f6f6f6;
@header-background: #444;
@header-foreground: #fff;
@nav-background: #fafafa;
@nav-highlight: #fff;
@album-background: #fafafa;
@text-color: #444;
@text-light: #999;
@borders: #ddd;
@mobile-trigger: 900px;
```

<br />

<div style="margin: 2em 0; text-align: center;">
  <a class="btn btn-cta-primary" href="/docs/deployment">Next: deployment</a>
</div>
