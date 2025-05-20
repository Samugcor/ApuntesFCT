#apuntes #css #howto 
___
```css
#menu{

    position: fixed;
    top: 2vh;
    left: 50%;
    transform: translateX(-50%);
    background: white;
    padding: 0.3%;
    border-radius: 10px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    display: flex;
    gap: 0.3vw;
    z-index: 999;

}
```

## position: fixed;

- **Fixes the element to the viewport** (the screen), so it stays in place when the user scrolls.
- Without `fixed`, it would move with the content (default is `static`).
- This is key to making a "floating" UI component.

## left: 50%;

- Moves the left edge of the element to the horizontal center of the screen.
- But that alone doesn’t center the whole element—just its left edge.

## transform: translateX(-50%);

- Shifts the element left by 50% of its own width, effectively centering it.
- Works with left: 50% to center the entire element, not just align its left side.
- This trick is common for centering elements horizontally with unknown widths.

