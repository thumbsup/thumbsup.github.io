---
layout: default
title: Themes
---

## Themes

The `--theme` flag allows you to select a style for the generated gallery.
Here are the current themes available:

<ul class="theme-gallery">
  <li><img src="/public/images/theme-default.png" /></li>
  <li><img src="/public/images/theme-placeholder.png" /></li>
  <li><img src="/public/images/theme-placeholder.png" /></li>
</ul>

To submit a theme, please [raise an issue on Github here](https://github.com/thumbsup/thumbsup).

### Configuration

Some themes have [LESS](http://lesscss.org/) variables that you can customise.
Check [THEMES.md](THEMES.md) for more details.
Simply use the `--css` option and pass a LESS file with your values, e.g.

```less
// thumbsup --css custom.less

@myvariable: #cef9b6;
```

<br />

<div style="margin: 2em 0; text-align: center;">
  <a class="btn btn-cta-primary" href="/docs/deployment">Next: deployment</a>
</div>
