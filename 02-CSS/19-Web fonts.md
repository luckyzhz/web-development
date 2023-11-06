# 19-Web fonts

> To learn how to apply web fonts to a web page, using either a third party service, or by writing your own code.

---

## Web fonts

CSS allows you to specify font files, available on the web, to be downloaded along with your website as it's accessed.

```css
@font-face {
    font-family: "myFont";
    src: url("myFont.woff2");
}

html {
    font-family: "myFont", "Bitstream Vera Serif", serif;
}
```

---

## Using an online font service

Online font services generally store and serve fonts for you so you don't have to worry about writing the `@font-face` code.

- [Google Fonts](https://fonts.google.com/)

---

## @font-face in more detail

```css
@font-face {
    font-family: "zantrokeregular";
    src:
        url("zantroke-webfont.woff2") format("woff2"),
        url("zantroke-webfont.woff") format("woff");
    font-weight: normal;
    font-style: normal;
}
```

- `font-family`: This line specifies the name you want to refer to the font as.
- `src`: These lines specify the paths to the font files to be imported into your CSS (the `url` part), and the format of each font file (the `format` part).
- `font-weight`/`font-style`: These lines specify what weight the font has and whether it is italic or not.



---

?> {docsify-updated}