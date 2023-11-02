# 05-Cascade layers

> To learn how cascade layers work.

---

## Overview of cascade layers

Similar to how we have six levels of priority based on origin and importance, cascade layers enable us to create **sub-origin** level of priority within any of those origins. Cascade layers enable the prioritizing of entire stylesheets over other stylesheets, without having to worry about specificity between these sub-origins.

In normal origin buckets, layers are sorted in the **order** of each layer's **creation**. The order of **precedence** is from the **first** layer created to the **last**, followed by **unlayered** normal styles. This order is **inverted** for **important** styles.

Cascade layers allow the creation of nested layers. Each cascade layer can contain nested layers.

---

## Creating cascade layers

Layers can be created using any one of the following methods:
- The `@layer` statement at-rule
  - Declare layers using `@layer` followed by the names of one or more layers. This creates named layers without assigning any styles to them.
- The `@layer` block at-rule
  - All styles within a block are added to a named or unnamed layer.
- The `@import` rule with the `layer` keyword or `layer()` function
  - Assign the contents of the imported file into that layer.

If no layer name is provided in the `@layer` at-rule or `@import` with `layer()`, a new anonymous (unnamed) layer is created.

?> ⚠️ **Note**: The order of precedence of layers is the order in which they are created. Styles not in a layer, or "unlayered styles", cascade together into a **final implicit layer**.

### The @layer statement at-rule for named layers

Declaring layers using `@layer` followed by the names of one or more layers without assigning any styles is one way to **define the layer order**.

The following at-rule declares three layers, in the order listed:

```css
@layer theme, layout, utilities;
```

You will often want to have your first line of CSS be this `@layer` declaration (with layer names that make sense for your site, of course) to have full control over layer ordering.

### The @layer block at-rule for named and anonymous layers

If a layer with the specified name does not already exist, a **new** layer will be created. If a layer with the specified name already exists, the styles are added to the **previously existing** layer.

If no name is specified while creating a block of styles using `@layer`, the styles in the at-rule will be added to a **new** anonymous layer.

```css
/* unlayered styles */
body {
    color: #333;
}

/* creates the first layer: `layout` */
@layer layout {
    main {
        display: grid;
    }
}

/* creates the second layer: an unnamed, anonymous layer */
@layer {
    body {
        margin: 0;
    }
}

/* creates the third and fourth layers: `theme` and `utilities` */
/* layer `layout` has already been created */
@layer theme, layout, utilities;

/* adds styles to the already existing `layout` layer */
@layer layout {
    main {
        color: #000;
    }
}

/* creates the fifth layer: an unnamed, anonymous layer */
@layer {
    body {
        margin: 1vw;
    }
}
```

In the above CSS, we created five layers: `layout`, `<anonymous(01)>`, `theme`, `utilities`, and `<anonymous(02)>` – in that order - with a sixth, **implicit** layer of unlayered styles contained in the `body` style block. The layer order is the order in which the layers are created, with the implicit layer of unlayered styles always being last. *There is no way to change the layer order once created*.

Anonymous layers are created by assigning styles to a layer without naming the layer. *Styles can be added to an unnamed layer only at the time of its creation*.

?> ⚠️ **Note**: Subsequent use of `@layer` with no layer name creates additional unnamed layers; it does **not** append styles to a previously existing unnamed layer.

#### Layer creation and media queries

If you define a layer using `media` or `feature` queries, and the media is not a match or the feature is not supported, the layer is not created.

The example below shows how changing the size of your device or browser may change the layer order:

```css
@media (min-width: 50em) {
    @layer site;
}

@layer page {
    h1 {
        text-decoration: overline;
        color: red;
    }
}

@layer site {
    h1 {
        text-decoration: underline;
        color: green;
    }
}
```

In wide screens, the `site` layer is declared in the first line, meaning `site` has less precedence than `page`. Otherwise, `site` has precedence over `page` because it is declared later on narrow screens.

### Importing style sheets into named and anonymous layers with @import

The `@import` rule allows users to import style rules from other style sheets either directly into a CSS file or into a `<style>` element.

When importing stylesheets, the `@import` statement must be defined **before any CSS styles** within the stylesheet or `<style>` block. The `@import` statement must come first, before any styles, but **can be preceded** by an `@layer` at-rule that creates one or more layers **without assigning any styles** to the layers.

You can import a stylesheet into a **named** layer, a **nested** named layer, or an **anonymous** layer. The following layer imports the style sheets into a `components` layer, a nested `dialog` layer within the `components` layer, and an un-named layer, respectively:

```css
@import url("components-lib.css") layer(components);
@import url("dialog.css") layer(components.dialog);
@import url("marketing.css") layer();
```

You can import styles and create layers based on specific conditions using *media queries* and *feature queries*. The following imports a style sheet into an `international` layer only if the browser supports `display: ruby`, and the file being imported is dependent on the width of the screen:

```css
@import url("ruby-narrow.css") layer(international) supports(display: ruby) and (width < 32rem);
@import url("ruby-wide.css") layer(international) supports(display: ruby) and (width >=32rem);
```

---

## Creating nested cascade layers

Nested layers can be created using the same methods as described for regular layers. For example, they can be created using `@layer` at-rule followed by the names of one or more layers, using a dot (`.`) notation. Multiple dots and layer names signify multiple nesting.

To add styles to a named nested layer, use the dot notation:

```css
@layer example.layout {
    main {
        width: 50vw;
    }
}
```

## Determining the precedence based on the order of layers

### Precedence order of regular cascade layers

```css
@import url(A.css) layer(firstLayer);
@import url(B.css) layer(secondLayer);
@import url(C.css);
```

The above code creates two named layers and one unnamed layer. Let us assume that the three files (`A.css`, `B.css`, and `C.css`) do not contain any additional layers within them. The following list shows where styles declared inside and outside of these files will be sorted from *least (1)* precedence to *highest (10)*:
1. `firstLayer` normal styles (`A.css`)
2. `secondLayer` normal styles (`B.css`)
3. **unlayered** normal styles (`C.css`)
4. **inline** normal styles
5. **animating** styles
6. **unlayered important** styles (`C.css`)
7. `secondLayer` **important** styles (`B.css`)
8. `firstLayer` **important** styles (`A.css`)
9. **inline important** styles
10. **transitioning** styles

### Precedence order of nested cascade layers

The cascade precedence order for nested layers is similar to that of regular layers, but contained within the layer. The precedence order is based on the order of nested layer creation. Non-nested styles in a layer have precedence over nested normal styles, with the precedence order reversed for important styles. Specificity weight between nested layers does not matter, though it does matter for conflicting styles within a nested layer.



---

?> {docsify-updated}