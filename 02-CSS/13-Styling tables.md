# 13-Styling tables

> To learn how to effectively style HTML tables.

---

## A typical HTML table

Here is a table about famous punk bands from the UK ([final effect preview](https://mdn.github.io/learning-area/css/styling-boxes/styling-tables/punk-bands-complete.html)):

```html
<table>
    <caption>
        A summary of the UK's most famous punk bands
    </caption>
    <thead>
        <tr>
            <th scope="col">Band</th>
            <th scope="col">Year formed</th>
            <th scope="col">No. of Albums</th>
            <th scope="col">Most famous song</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">Buzzcocks</th>
            <td>1976</td>
            <td>9</td>
            <td>Ever fallen in love (with someone you shouldn't've)</td>
        </tr>
        <tr>
            <th scope="row">The Clash</th>
            <td>1976</td>
            <td>6</td>
            <td>London Calling</td>
        </tr>

        <!-- several other great bands -->

        <tr>
            <th scope="row">The Stranglers</th>
            <td>1974</td>
            <td>17</td>
            <td>No More Heroes</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <th scope="row" colspan="2">Total albums</th>
            <td colspan="2">77</td>
        </tr>
    </tfoot>
</table>
```

---

## Spacing and layout

```css
/* spacing */

table {
    table-layout: fixed;
    width: 100%;
    border-collapse: collapse;
    border: 3px solid purple;
}

thead th:nth-child(1) {
    width: 30%;
}

thead th:nth-child(2) {
    width: 20%;
}

thead th:nth-child(3) {
    width: 15%;
}

thead th:nth-child(4) {
    width: 35%;
}

th,
td {
    padding: 20px;
}
```

- Setting `table-layout: fixed` for table makes the table behave a bit more predictably. With `table-layout: fixed`, you can size your columns according to the width of their headings.
- With `border-collapse: collapse;` set, the borders collapse down into one, which looks much better.

---

## Some simple typography

We can find fonts on [Google Fonts](https://fonts.google.com/).

To introduce fonts, just add the `<link>` element into your HTML head like this:

```html
<link href="https://fonts.googleapis.com/css?family=Rock+Salt" rel="stylesheet">
```

Now add the following CSS into your `style.css` file, below the previous addition:

```css
/* typography */

html {
    font-family: "helvetica neue", helvetica, arial, sans-serif;
}

thead th,
tfoot th {
    font-family: "Rock Salt", cursive;
}

th {
    letter-spacing: 2px;
}

td {
    letter-spacing: 1px;
}

tbody td {
    text-align: center;
}

tfoot th {
    text-align: right;
}
```

---

## Graphics and colors

```css
/* graphics and colors */

thead,
tfoot {
    background: url(leopardskin.jpg);
    color: white;
    text-shadow: 1px 1px 1px black;
}

thead th,
tfoot th,
tfoot td {
    background: linear-gradient(to bottom,
            rgba(0, 0, 0, 0.1),
            rgba(0, 0, 0, 0.5));
    border: 3px solid purple;
}
```

---

## Zebra striping

```css
/* zebra striping */

tbody tr:nth-child(2n+1) {
    background-color: #ff33cc;
}

tbody tr:nth-child(2n) {
    background-color: #e495e4;
}

tbody tr {
    background-image: url(noise.png);
}
```

---

## Styling the caption

```css
/* caption */

caption {
    font-family: "Rock Salt", cursive;
    padding: 20px;
    font-style: italic;
    caption-side: bottom;
    color: #666;
    text-align: right;
    letter-spacing: 1px;
}
```

With `caption-side: bottom`, the caption is positioned on the bottom of the table.

Here is a screenshot of the final effect after apply all the CSS above:

![](../_assets/_images/UK%20punk%20bands.png ':size=800')

---

## Summary

A quick list of the most useful points illustrated above:

- Make your table markup as simple as possible, and keep things flexible, e.g. by using percentages, so the design is more responsive.
- Use `table-layout: fixed;` to create a more predictable table layout that allows you to easily set column widths by setting `width` on their headings (`<th>`).
- Use `border-collapse: collapse;` to make table elements borders collapse into each other, producing a neater and easier to control look.
- Use `<thead>`, `<tbody>`, and `<tfoot>` to break up your table into logical chunks and provide extra places to apply CSS to, so it is easier to layer styles on top of one another if required.
- Use **zebra striping** to make alternative rows easier to read.
- Use `text-align` to line up your `<th>` and `<td>` text, to make things neater and easier to follow.



---

?> {docsify-updated}