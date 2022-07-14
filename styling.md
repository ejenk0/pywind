# Styling

This page outlines style attributes and their possible values for elements.

## The style string

The style string can be passed to the `pywind.Style` component of an element to be converted into styling attributes. It is a semicolon separated list of style attributes and values (like a combination of in-line CSS and TailwindCSS).

For example:

```python
"background-colour: (255, 0, 0); row; height: 10%; padding: 2px;"
```

## Quick styling reference

Quick reference of the available styling attributes:

Attribute | Description | Possible values
--- | --- | ---
[`width`](#width) | Sets the width of the element. | % or px
[`height`](#height) | Sets the height of the element. | % or px
[`direction`](#direction) | Sets the direction of child elements. | `row` or `column`
[`justify-content`](#justify--justify-content) | Sets the primary axis alignment of the element's children. | `start`, `end`, `center`, `equally-spaced`
[`align-items`](#align--align-items) | Sets the cross-axis alignment of the element's children. | `start`, `end`, `center`
[`padding`](#padding-1) | Sets the paddings of the element. | % or px (`all`), (`horiz`, `vert`), (`left`, `top`, `right`, `bottom`)
[`margin`](#margin-1) | Sets the margins of the element. | % or px (`all`), (`horiz`, `vert`), (`left`, `top`, `right`, `bottom`)
[`font`](#font--font-family) | The font family of the element. | str (sysfont or relative .ttf font path)
[`font-size`](#font-size) | The font size of the element. | % or px
[`text-colour`](#text-colour--text-color) | The text colour of the element. | Hex, RGB(A) or name
[`background-colour`](#background-colour--background-color) | The background colour of the element. | Hex, RGB(A) or name
[`border-colour`](#border-colour--border-color) | The border colour of the element. | Hex, RGB(A) or name
[`border`](#border--border-width) | The border width of the element. | px
[`border-radius`](#border-radius--rounding) | The border radius of the element. | px
[`colour-key`](#colour-key--color-key) | The transparency colour key of the element. | Hex, RGB(A) or name
[`positioning`](#positioning) | The positioning style of the element | `auto` or `absolute`
[`pos`](#pos) | The position of an absolutely positioned element | `left`, `top` (% or px)
[`hover: attr: val;`](#hover) | Hovered styling. | Any attribute-style pair
[`active: attr: val;`](#active) | Active (clicked) styling. | Any attribute-style pair

All attributes also support `inherit` as a value. This means that the value of the attribute is inherited from the **calculated** value on the parent element (percentages are calculated on the parent before being inherited).

Percentage based values are computed based on the parent element's size. A parent Element must be present on the Style for these to work, otherwise a warning will be raised and the default value will be used.

Additionally, many styling attributes include aliases for internationalised versions of the attribute name, or for the sake of similarity with the CSS equivalent.

## Positioning Attributes

### `positioning`

Default value: `auto`

The positioning attribute is used to set the positioning style of the element. `auto` is the default value for most elements and means the element will get its position from its parent element (e.g. it will take its correct place in a row or column).

`absolute` will set the element to be positioned absolutely relative to its parent and won't be considered in the row or column layout of the parent element. An absolutly positioned element should have a set `pos` value.

**An absolutely positioned element can have either an `pywind.Element` or a `pygame.Surface` as a parent.**

### `pos`

Default value: `0px 0px`

The `pos` value is **only used for absolutely positioned elements**. It sets the position of the element relative to its parent rect either in absolute pixels or as a percentage of the parent element's width/height.

Additionally, `pos-topleft`, `pos-midtop`, `pos-topright`, `pos-midright`, `pos-bottomright`, `pos-midbottom`, `pos-bottomleft`, `pos-midleft`, `pos-center` are also available to position based on other parts of the elements Rect.

```python
"pos: 10px 10px" # 10px from the left and 10px from the top
"pos-center: 50% 50%" # centered inside the parent element
"pos-topright: 100% 5px" # against the right edge of the parent element 5px from the top
```

## Child Alignment Attributes

These attributes are used to align and justify children of an element.

### `direction`

Default value: `row`

The direction attribute is used to set the direction of the children of the element. `row` is the default value and means the children will be laid out in a row. `column` means the children will be laid out in a column.

```python
"direction: row;" # children will be laid out in a row
"direction: column;" # children will be laid out in a column
```

### `justify` / `justify-content`

Default value: `start`

The justify attribute is used to align children of an element along the primary axis. For rows, this means horizontal alignment and for columns, this means vertical alignment. Valid values are: `start`, `end`, `center` and `equally-spaced`.

```python
"justify: start;" # Aligns children along the primary axis to the start of the element.
"justify: end;" # Aligns children along the primary axis to the end of the element.
"justify: center;" # Centers children along the primary axis.
```

### `align` / `align-items`

Default value: `center`

The align attribute is used to align children of an element along the cross-axis. For rows, this means vertical alignment and for columns it means horizontal alignment. Valid values are: `start`, `end` and `center`.

```python
"align: center;" # Aligns children centrally along the cross-axis.
"align: start;" # Aligns children to the start of the cross-axis. (For rows, this means top-aligned and for columns, this means left-aligned.)
"align: end;" # Aligns children to the end of the cross-axis. (For rows, this means bottom-aligned and for columns, this means right-aligned.)
```

## Size Attributes

The size attributes are used to set both fixed and relative sizes of elements.

### `height`

Default value: `100%`

The value of the `height` attribute is a percentage or a fixed size. If a percentage is given, the height of the element is computed based on the height of its parent. If a fixed size is given, the height of the element is set to that size.

```python
"height: 10%;" # height is 10% of the parent's height
"height: 100px;" # height is always 100px
"height: 100%;" # height fill the parent's height minus padding
```

### `width`

Default value: `100%`

The value of the `width` attribute is a percentage or a fixed size. If a percentage is given, the width of the element is computed based on the width of its parent. If a fixed size is given, the width of the element is set to that size.

```python
"width: 10%;" # width is 10% of the parent's width
"width: 100px;" # width is always 100px
"width: 100%;" # width fill the parent's width minus padding
```

## Padding

The padding attribute is used to set internal padding of an element. It will be considered when rendering child elements. Padding can be set individually for each side of an element.

### `padding`

Default value: `0px`

The value of the padding attribute can be one, two or four values, each being either a fixed pixel amount or a percentage of the elements height/width.

```python
"padding: 2px" # 2px of padding on all sides
"padding: 1% 0.5%" # 1% padding on the left and right, 0.5% padding on the top and bottom
"padding: 2px 0.5% 1px 0.2%" # left, top, right, bottom = 2px, 0.5%, 1px, 0.2%
```

## Margin

The margin attribute is used to offset an element's rendered content by some amount. An element with margin will take up the same amount of space in the parent element as one without.

### `margin`

Default value: `0px`

The margin attribute's value is written in the same way as the padding attribute. Percentages, like with padding, relate to the **element's** height/width, not its parent. A 1% margin will be 1% of the element's height/width.

```python
"margin: 2px" # 2px of margin on all sides
"margin: 1% 0.5%" # 1% margin on the left and right, 0.5% margin on the top and bottom
"margin: 2px 0.5% 1px 0.2%" # left, top, right, bottom = 2px, 0.5%, 1px, 0.2%
```

## Colours

The following attributes are used to set the colours of different parts of an element. Generally, the attribute name can be written in British or American english, and the value can be anything supported by the pygame.Color class (RGB, Hex, colour string etc.)

### `text-colour` / `text-color`

Default value: `inherit`

The text colour attribute sets the text colour of an element.
Its value is converted to a pygame.Color object.

```python
"text-colour: #ff0000;" # text colour is red
"text-color: (0, 255, 0);" # text colour is green
"text-colour: blue;" # text colour is blue
```

### `background-colour` / `background-color`

Default value: `white`

The background colour attribute sets the background fill colour of an element.
Its value is converted to a pygame.Color.

If the background colour is set to `transparent`, the element will be filled with the current colour-key.

```python
"background-colour: #ff0000;" # background fill colour is red
"background-color: (0, 255, 0);" # background fill colour is green
"background-colour: blue;" # background fill colour is blue
"background-colour: transparent;" # background fill colour is the current colour-key
```

### `border-colour` / `border-color`

Default value: `black`

The border colour attribute sets the border colour of an element. Its value is passed to the pygame.Color constructor.

```python
"border-colour: #ff0000;" # border colour is red
"border-color: (0, 255, 0);" # border colour is green
"border-colour: blue;" # border colour is blue
```

### `colour-key` / `color-key`

Default value: `(220, 221, 222)`

The colour-key attribute is used for the transparent areas of the element's image. The default is arbitrarily chosen and should only be overwritten if the element's image contains `(220, 221, 222)`.

A notable exception is the Image class which defaults this attribute to `None` and therefore don't support transparency by default. This is due to the fact that images may often contain traces of the default colour key.

## Border

The border attributes set the width and radius of the element's border. Border is not included in size calculations.

### `border` / `border-width`

Default value: `0px`

The border / border-width attribute sets the width of the element's border either in pixels.

```python
"border: 2px;" # border width is 2px
"border-width: 1px;" # border width is 1px
```

### `border-radius` / `rounding`

Default value: `0px`

The border-radius / rounding attribute sets the radius (rounding) of the element.

```python
"border-radius: 2px;" # border radius is 2px
"rounding: 1px;" # border radius is 1px
```

## Font

Attributes related to the font of the text of an element.

### `font` / `font-family`

Default value: `inherit`

The font attribute sets the font family of the element. If it is a font available on the current system or it is a tuple it is passed directly to the `pygame.font.SysFont` constructor.

Otherwise it is assumed to be font file path (`myfont.ttf`) and is joined with the current working directory and passed to the `pygame.font.Font` constructor. Should this fail a warning is raised and the default pygame font is used.

```python
"font: Arial;" # font is Arial
"font: myfont.ttf;" # font is myfont.ttf
```

### `font-size`

Default value: `inherit`

The font-size attribute sets the size of the font. It can be a fixed pixel size or a percentage of the element's height.

```python
"font-size: 10px;" # font size is 10px
"font-size: 10%;" # font size is 10% of the element's height
```

## Interaction

The interaction attributes relate to the styling of the element as it is interacted with.

### `hover`

`hover` acts like a decorator. It is used to add a styling behaviour to an element when it is hovered over and not being clicked.

```python
"hover: background-colour: #ff0000;" # background fill colour is red when hovered over
"hover: background-colour: #00ff00; hover: font-size: 20px;" # background fill colour is green and font size is 20px when hovered over
```

### `active`

`active` acts like a decorator. It is used to add a styling behaviour to an element when it is being clicked on or when it remains active after being clicked (such as radio buttons and focused input fields).

```python
"active: background-colour: #ff0000;" # background fill colour is red when active
"active: background-colour: #00ff00; active: font-size: 20px;" # background fill colour is green and font size is 20px when active
```

### `cursor`

Default value: `None`

`cursor` sets the cursor to be used when the element is hovered over. This will be passed directly to the `pygame.mouse.set_cursor` function unless it is `None`.

`hover: cursor:` is equivalent to just `cursor:`, but `active: cursor:` can still be set for a different cursor on an active element.

```python
f"cursor: {pygame.SYSTEM_CURSOR_HAND};" # cursor is set to a hand when this element is hovered over
```
