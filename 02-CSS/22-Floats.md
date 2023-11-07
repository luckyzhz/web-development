# 22-Floats

> To learn how to create floated features on webpages and to use the clear property as well as other methods for clearing floats.

---

## Floating elements

The `float` CSS property places an element on the left or right side of its container, allowing text and inline elements to wrap around it.

```css
.box {
    float: left;
    margin-right: 15px;
    width: 150px;
    height: 100px;
    border-radius: 5px;
    background-color: rgb(207, 232, 220);
}
```

The value of the `float` property can be:

- `none`
- `left`
- `right`
- `inline-start`
- `inline-end`

While we can add a margin to the float to push the text away, we can't add a margin to the text to move it away from the float. This is because a floated element **is taken out of normal flow** and the boxes of the **following items actually run behind the float**.

## Clearing floats

The `clear` CSS property sets whether an element must be moved below (cleared) floating elements that precede it. The `clear` property applies to floating and non-floating elements.

```css
.cleared {
    clear: left;
}
```

The value of the `clear` property can be:

- `none`
- `left`
- `right`
- `both`
- `inline-start`
- `inline-end`



---

?> {docsify-updated}