# 10-HTML tables

> To learn about more advanced HTML table features. 

---

## Styling tables with `<col>`

`<col>` elements are specified inside a `<colgroup>` container just below the opening `<table>` tag.

```html
<table style="text-align: center;">
    <colgroup>
        <col style="background-color: gray">
        <col span="2" style="background-color: yellow">
    </colgroup>
    <tr>
        <th>Activity 1</th>
        <th>Activity 2</th>
        <th>Activity 3</th>
    </tr>
    <tr>
        <td rowspan="2">Homework</td>
        <td colspan="2">Swimming</td>
    </tr>
    <tr>
        <td>Basketball</td>
        <td>Football</td>
    </tr>
</table>
```

The example above will be rendered like this:

![](../_assets/_images/styling%20tables%20with%20col.svg ':size=300')

---

## Adding a caption to your table with `<caption>`

You can give your table a caption by putting it inside a `<caption>` element and nesting that inside the `<table>` element. You should put it just below the opening `<table>` tag.

```html
<table>
    <caption>
        Dinosaurs in the Jurassic period
    </caption>

    …
</table>
```

---

## Adding structure with `<thead>`, `<tfoot>`, and `<tbody>`

We can use `<thead>`, `<tfoot>`, and `<tbody>` to mark up a header, footer, and body section for the table.

These elements don't make the table any more accessible to screen reader users, and don't result in any visual enhancement on their own. They are however very useful for styling and layout — acting as useful hooks for adding CSS to your table.

For example, in the case of a long table you could make the table header and footer repeat on every printed page, and you could make the table body display on a single page and have the contents available by scrolling up and down.

?> ⚠️ **Note**: `<tbody>` is always included in every table, implicitly if you don't specify it in your code. To check this, open up one of your previous examples that doesn't include `<tbody>` and look at the HTML code in your browser developer tools — you will see that the browser has added this tag for you. You might wonder why you ought to bother including it at all — you should, because it gives you more control over your table structure and styling.

---

## Nesting Tables

It is possible to nest a table inside another one, as long as you include the complete structure, including the `<table>` element.



---

?> {docsify-updated}