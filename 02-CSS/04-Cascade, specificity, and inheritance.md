# 04-Cascade, specificity, and inheritance

> To learn about the cascade and specificity, and how inheritance works in CSS.

---

## Understanding inheritance

### Controlling inheritance

CSS provides five special universal property values for controlling inheritance. **Every CSS property** accepts these values.

- `inherit`
  - Sets the property value applied to a selected element to be the same as that of its **parent** element. Effectively, this "turns on inheritance".
- `initial`
  - Sets the property value applied to a selected element to the initial value of that **property**.
- `revert`
  - Resets the property value applied to a selected element to the **browser**'s default styling rather than the defaults applied to that property. This value acts like `unset` in many cases.
- `revert-layer`
  - Resets the property value applied to a selected element to the value established in a **previous cascade layer**.
- `unset`
  - Resets the property to its natural value, which means that if the property is naturally inherited it acts like `inherit`, otherwise it acts like `initial`.

### Resetting all property values

The CSS shorthand property `all` can be used to apply one of these inheritance values to (almost) all properties at once. Its value can be any one of the inheritance values (`inherit`, `initial`, `revert`, `revert-layer`, or `unset`). It's a convenient way to undo changes made to styles so that you can get back to a known starting point before beginning new changes.

In the below example, we have two `blockquotes`. The first has styling applied to the blockquote element itself. The second has a class applied to the blockquote, which sets the value of `all` to `unset`.

```html
<style>
    blockquote {
        background-color: orange;
        border: 2px solid blue;
    }

    .fix-this {
        all: unset;
    }
</style>

<blockquote>
    <p>This blockquote is styled</p>
</blockquote>

<blockquote class="fix-this">
    <p>This blockquote is not styled</p>
</blockquote>
```

---

## Understanding the cascade

We will now look at how **cascade** defines which CSS rules apply when more than one style block apply the same property, but with different values, to the same element.

There are three factors to consider, listed here in increasing order of importance. Later ones overrule earlier ones:
1. **Source order**
2. **Specificity**
3. **Importance**

### Source order

If you have more than one rule, all of which have exactly the same weight, then the one that comes last in the CSS will win. Source order only matters when the specificity weight of the rules is the same.

### Specificity

Essentially a value in points is awarded to different types of selectors, and adding these up gives you the weight of that particular selector, which can then be assessed against other potential matches.

The amount of specificity a selector has is measured using three different values (or components), which can be thought of as **ID**, **CLASS**, and **ELEMENT** columns in the **hundreds**, **tens**, and **ones** place:

- **Identifiers**: Score one in this column for each `ID` selector contained inside the overall selector.
- **Classes**: Score one in this column for each `class` selector, `attribute` selector, or `pseudo-class` contained inside the overall selector.
- **Elements**: Score one in this column for each `element` selector or `pseudo-element` contained inside the overall selector.

?> ⚠️ **Note**: The universal selector (`*`), combinators (`+`, `>`, `~`, ` `), and specificity adjustment selector (`:where()`) along with its parameters, have no effect on specificity.

The negation (`:not()`), relational selector (`:has()`), the matches-any (`:is()`) pseudo-classes, and *CSS nesting* themselves don't add to specificity, but their **parameters** or **nested rules** do. The specificity weight that each contributes to the specificity algorithm is the specificity weight of the selector in the parameter or nested rule with the **greatest weight**.

The following table shows a few isolated examples:

| Selector                                  | Identifiers | Classes | Elements | Total specificity |
| :---------------------------------------- | :---------- | :------ | :------- | :---------------- |
| `h1`                                      | 0           | 0       | 1        | 0-0-1             |
| `h1 + p::first-letter `                   | 0           | 0       | 3        | 0-0-3             |
| `li > a[href*="en-US"] > .inline-warning` | 0           | 2       | 2        | 0-2-2             |
| `#identifier`                             | 1           | 0       | 0        | 1-0-0             |
| `button:not(#mainBtn, .cta)`              | 1           | 0       | 1        | 1-0-1             |

?> ⚠️ **Note**: Each selector type has its own level of specificity that **cannot be overwritten** by selectors with a lower specificity level. For example, a *million* **class** selectors combined would not be able to overwrite the specificity of *one* **id** selector.

### Inline styles

Inline styles, that is, the style declaration inside a `style` attribute, take precedence over all normal styles, no matter the specificity. Such declarations don't have selectors, but their specificity can be construed as `1-0-0-0`; always more than any other specificity weight no matter how many IDs are in the selectors.

### !important

There is a special piece of CSS that you can use to overrule all of the above calculations, **even inline styles** - the `!important` flag.

```css
.better {
    border: none !important;
}
```

!> **Warning**: The `!important` flag changes the way the cascade normally works, so it can make debugging CSS problems really hard to work out, especially in a large stylesheet.

---

## The effect of CSS location

Finally, it is important to note that the precedence of a CSS declaration depends on what stylesheet and cascade layer it is specified in.

### Order of overriding declarations

Conflicting declarations will be applied in the following order, with later ones overriding earlier ones:

1. Declarations in user **agent** style sheets (e.g., the browser's default styles, used when no other styling is set).
2. Normal declarations in **user** style sheets (custom styles set by a user).
3. Normal declarations in **author** style sheets (these are the styles set by us, the web developers).
4. Important declarations in **author** style sheets.
5. Important declarations in **user** style sheets.
6. Important declarations in user **agent** style sheets.

We can note that the order of precedence is inverted for styles flagged with `!important`.

### Order of cascade layers

When you declare CSS in cascade layers, the order of precedence is determined by **the order in which the layers are declared**. CSS styles declared outside of any layer are combined together, in the order in which those styles are declared, into an **unnamed layer**, as if it were the **last declared layer**. With competing normal (not important) styles, **later layers take precedence over earlier defined layers**.

For styles flagged with `!important`, however, the order is **reversed**, with important styles in earlier layers taking precedence over important styles declared in subsequent layers or outside of any layer.

Specificity between layers doesn't matter, but specificity within a single layer still does.

```css
<style>
    @layer firstLayer, secondLayer;

    p { /* 0-0-1 */
        background-color: red;
    }

    @layer firstLayer {
        p#addSpecificity { /* 1-0-1 */
            background-color: green;
        }
    }

    @layer secondLayer {
        #addSpecificity { /* 1-0-0 */
            background-color: blue;
        }
    }
</style>

<p id="addSpecificity">My background finally is red.</p>
```



---

?> {docsify-updated}