# Godot-CSS-Theme

Converts CSS to Godot Themes.

The goal is to make theme creating easier and more reusable. Using CSS you also have the advantage to use preprocessors like [SASS](https://sass-lang.com/). Since using normal CSS variables with `var()` is not supported (yet?).

## Supported Features

Generally all properties of a Godot Theme should be supported. The program uses custom css variables to set values.

The node_type is used like a tag to decide which node to style (e.g. `Button` or `CheckBox`).

The structure for a statement is `--{TYPE}-{PROPERTY}: {VALUE}` 
The only exception is for setting `styles`. They need a special type definition like `--styles-{PROPERTY}-type: {VALUE}`. See [syntax](#syntax)

### Syntax
 - `--{TYPE}-{PROPERTY}: {VALUE}`
    - `{TYPE}` - `colors`, `const`, `fonts`, `styles` 
    - `{PROPERTY}` - anything the node_type supports
    - `{VALUE}` - anything `str2var()` supports, hex values, `url()`
 - `--styles-{PROPERTY}-type` values: `Empty`, `Flat`, `Line`, `Texture`
 - external resources are specified with `url()`.
    - `url(res://file.txt)` or `url(/file.txt)` - absolute path
    - `url(file.txt)` - relative path to css file


### Example:
```css
Button {
    --colors-font-color: #000;
    --colors-font-color-disabled: Color(0, 0, 0, 0.5);

    --const-hseparation: 5;

    --fonts-font: url(res://font.tres);

    --styles-normal-type: Flat;
    --styles-normal-bg-color: #FFF;
}
```

## How to use

`godot -s addons/godot-css-theme/convert.gd --input="res://theme.css" --output="res://theme.tres"`

## Problems
 - Using colors with words like `red` or `blue` does not work. Either use hex `#000` or native gdscript `Color(0, 0, 0, 1)`
 - Godot might have to be closed before generating. Otherwise it might rewrite some values
