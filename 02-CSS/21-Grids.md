# 21-Grids

> To understand the fundamental concepts of grid layout as well as how to implement it with CSS Grid.

---

## What is grid layout?

A grid will typically have **columns**, **rows**, and then gaps between each row and column. The gaps are commonly referred to as **gutters**.

![](../_assets/_images/grid.png ':size=800')

Here is the html used to demonstrate grid layout:

```html
<style>
    * {
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }

    .container {
        border: 1px red solid;
    }

    .item {
        border: 1px blue solid;
        border-radius: 4px;
        background-color: aqua;
        line-height: 2;
    }
</style>

<section class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
    <div class="item">7</div>
    <div class="item">8</div>
</section>
```

---

## Creating your grid in CSS

### Defining a grid

Define a grid layout by setting the value of the `display` property to `grid`. As in the case of flexbox, the `display: grid;` property transforms all the **direct children** of the container into **grid items**.

```css
.container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
}
```

Declaring `display: grid;` gives you a one column grid. To see something that looks more grid-like, we add three 200-pixel columns by declaring `grid-template-columns: 200px 200px 200px;`.

### Flexible grids with the fr unit

In addition to creating grids using *lengths* and *percentages*, we can use unit `fr`. The `fr` unit represents **one fraction** of the **available space** in the grid container to flexibly size grid rows and columns.

```css
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
}
```

You now have flexible tracks. The `fr` unit distributes space proportionally. You can also specify different positive values for your tracks like `grid-template-columns: 2fr 1fr 1fr;`.

You can **mix** `fr` units with **fixed length units**. In this case, the space needed for the fixed tracks is used up first before the remaining space is distributed to the other tracks.

?> ⚠️ **Note**: The `fr` unit distributes **available space**, not all space. Therefore, if one of your tracks has something large inside it, there will be less free space to share.

### Gaps between tracks

To create gaps between tracks, we use the properties:

- `column-gap` for gaps between columns
- `row-gap` for gaps between rows
- `gap` as a shorthand for both

```css
.container {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    gap: 10px;
}
```

These gaps can be any length unit or percentage, but not an `fr` unit.

### Repeating track listings

You can repeat all or merely a section of your track listing using the CSS `repeat()` function.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}
```

You'll now get three `1fr` tracks just as before. The first value passed to the `repeat()` function specifies the number of times you want the listing to repeat, while the second value is a **track listing**, which may be **one or more tracks** that you want to repeat.

### Implicit and explicit grids

Up to this point, we've specified only column tracks, but rows are automatically created to hold the content.

- **Explicit grid** is created using `grid-template-columns` or `grid-template-rows`.
- **Implicit grid** extends the defined explicit grid when content is placed outside that grid, such as into the rows by drawing additional grid lines.

By default, tracks created in the implicit grid are `auto` sized, which in general means that they're large enough to contain their content. If you wish to give implicit grid tracks a size, you can use the `grid-auto-rows` and `grid-auto-columns` properties.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: 100px;
    gap: 10px;
}
```

### The minmax() function

It might be better to have tracks that are **at least** 100 pixels tall and can still **expand** if more content becomes added.

The `minmax()` function lets us set a *minimum* and *maximum* size for a track, for example, `minmax(100px, auto)`. The minimum size is 100 pixels, but the maximum is `auto`, which will expand to accommodate more content.

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: minmax(100px, auto);
    gap: 10px;
}
```

### As many columns as will fit

Sometimes it's helpful to be able to ask grid to create as many columns as will fit into the container. We do this by setting the value of `grid-template-columns` using the `repeat()` function, but instead of passing in a number, pass in the keyword `auto-fit`.

```css
.container {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    grid-auto-rows: minmax(100px, auto);
    gap: 10px;
}
```

---

## Line-based placement

Our grid always has **lines** — these are numbered beginning with `1` and relate to the *writing mode* of the document.

To position items along these **lines**, we can specify the **start** and **end** lines of the **grid area** where an item should be placed. There are four properties we can use to do this:

- `grid-column-start`
- `grid-column-end`
- `grid-row-start`
- `grid-row-end`

These properties accept line numbers as their values, so we can specify that an item should start on line 1 and end on line 3, for example.

Alternatively, you can also use shorthand properties that let you specify the start and end lines simultaneously, separated by a forward slash `/`:

- `grid-column` shorthand for `grid-column-start` and `grid-column-end`
- `grid-row` shorthand for `grid-row-start` and `grid-row-end`

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-auto-rows: minmax(50px, auto);
    gap: 10px;
}

.item:nth-child(1) {
    /* use `-1` to target the last line */
    grid-column: 1 / -1;
    grid-row: 1;
}

.item:nth-child(2) {
    grid-column: 2 / 4;
    grid-row: 2 / 4;
}

.item:nth-child(5) {
    grid-column: 1;
    grid-row: 2 / 4;
}

.item:nth-child(7) {
    grid-column: 1 / -1;
    grid-row: 6;
}
```

?> ⚠️ **Note**: You can use the value `-1` to target the **end** column or row **line**, then count inwards from the end using **negative values**. Note also that lines count always from the edges of the **explicit grid**, not the implicit grid.

---

## Positioning with grid-template-areas

An alternative way to arrange items on your grid is to use the `grid-template-areas` property and give the various elements of your design a **name**.

```css
.container {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-auto-rows: minmax(50px, auto);
    gap: 10px;

    grid-template-areas:
        "header header"
        "navigation navigation"
        "sidebar content1"
        "sidebar content2"
        "sidebar content3"
        "sidebar content4"
        "footer footer";
}

.item:nth-child(1) {
    grid-area: header;
}

.item:nth-child(2) {
    grid-area: navigation;
}

.item:nth-child(3) {
    grid-area: sidebar;
}

.item:nth-child(n+4):nth-child(-n+7) {
    background-color: darksalmon;
    opacity: 0.5;
}

.item:nth-child(4) {
    grid-area: content1;
}

.item:nth-child(5) {
    grid-area: content2;
}

.item:nth-child(6) {
    grid-area: content3;
}

.item:nth-child(7) {
    grid-area: content4;
}

.item:nth-child(8) {
    grid-area: footer;
}
```

The rules for `grid-template-areas` are as follows:

- **Every cell** of the grid needs to be **filled**.
- To **span** across two cells, **repeat the name**.
- To leave a **cell empty**, use a `.` (period).
- Areas must be **rectangular** — for example, you can't have an L-shaped area.
- Areas can't be repeated in different locations.

---

## Nesting grids

It's perfectly OK to set a grid item to also be a grid container, so that its children are also laid out like grid.



---

?> {docsify-updated}