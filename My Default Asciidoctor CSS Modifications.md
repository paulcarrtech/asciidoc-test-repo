# DRAFT - My CSS Modifications to the Default Asciidoctor Stylesheet

I copied [asciidoctor-default.css](https://cdn.jsdelivr.net/gh/asciidoctor/asciidoctor@2.0/data/stylesheets/asciidoctor-default.css) into this repo.

To correct problems flagged by VS Code in asciidoctor-default.css, I made the following modifications.

## Modification #1

### Old Code

```css
button,html input[type=button],input[type=reset],input[type=submit]{-webkit-appearance:button;cursor:pointer}
```

### New Code

```css
button,html input[type=button],input[type=reset],input[type=submit]{-webkit-appearance:button;appearance:button;cursor:pointer}
```
I added `appearance:button;` to the original code.

## Modification #2

### Old Code

```css
#header,#content,#footnotes,#footer{width:100%;margin:0 auto;max-width:62.5em;*zoom:1;position:relative;padding-left:.9375em;padding-right:.9375em}
```

### New Code

```css
#header,#content,#footnotes,#footer{width:100%;margin:0 auto;max-width:62.5em;position:relative;padding-left:.9375em;padding-right:.9375em}
```

I removed `*zoom:1;` from the original code.