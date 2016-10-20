---
layout: default
title: thumbsup themes
---

The `--theme` flag allows you to select a style for the generated gallery.
Here are the current themes available:

<todo>

To submit a theme, please [raise an issue on Github here](https://github.com/thumbsup/thumbsup).

### Configuration

Some themes have [LESS](http://lesscss.org/) variables that you can customise.
Check [THEMES.md](THEMES.md) for more details.
Simply use the `--css` option and pass a LESS file with your values, e.g.

```less
// thumbsup --css custom.less

@myvariable: #cef9b6;
```
