# 07-Video and audio content

> To learn how to embed video and audio content into a webpage, and add captions/subtitles to video.

---

## The `<video>` element

Each `<source>` element has a `type` attribute. This is optional, but it is advised that you include it. The `type` attribute contains the [MIME type](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type) of the file specified by the `<source>`, and browsers can use the type to immediately skip videos they don't understand. The browser will go through the `<source>` elements and play the first one that it has the codec to support. If all the `<source>` elements are not supported, the **fallback content** will be shown.

```html
<video
  controls
  width="400"
  height="400"
  autoplay
  loop
  muted
  preload="auto"
  poster="poster.png">
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>
    Your browser doesn't support this video. Here is a
    <a href="rabbit320.mp4">link to the video</a> instead.
  </p>
</video>
```

---

## The `<audio>` element

The `<audio>` element works almost just like the `<video>` element.

```html
<audio controls>
  <source src="viper.mp3" type="audio/mp3">
  <source src="viper.ogg" type="audio/ogg">
  <p>
    Your browser doesn't support this audio file. Here is a
    <a href="viper.mp3">link to the audio</a> instead.
  </p>
</audio>
```

`<audio>`'s differences from `<video>` are as follows:
- The `<audio>` element doesn't support the `width`/`height` attributes — there is no visual component, so there is nothing to assign a width or height to.
- It also doesn't support the `poster` attribute — again, no visual component.

---

## Displaying video text tracks

- `<track>` should be placed within `<audio>` or `<video>`, but after all `<source>` elements.
- Use the `kind` attribute to specify whether the cues are `subtitles`, `captions`, or `descriptions`.
- Use `srclang` to tell the browser what language you have written the subtitles in.
- Add `label` to help readers identify the language they are searching for.

```html
<video controls>
  <source src="example.mp4" type="video/mp4" />
  <source src="example.webm" type="video/webm" />
  <track kind="subtitles" src="subtitles_es.vtt" srclang="es" label="Spanish">
</video>
```

For more details, including on how to add labels please read [Adding captions and subtitles to HTML video](https://developer.mozilla.org/en-US/docs/Web/Guide/Audio_and_video_delivery/Adding_captions_and_subtitles_to_HTML5_video).

---

?> {docsify-updated}