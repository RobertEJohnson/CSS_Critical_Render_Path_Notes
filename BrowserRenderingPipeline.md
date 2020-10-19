# Browser Rendering Pipeline

## Javascript

Pretty self explanatory here, with out going into too much depth.

## Style

1. HTML will parse into the Document Object Model.
2. CSS will parse into the CSS Object Model.
3. Both are combined into the Rendering Tree

At this point the browser knows which elements should be rendered on the page and which styles should be applied to them.

## Layout

This calculates the position and dimension of each layout

This means all relative measurements are converted into absolutes, so ```rem``` and ```em``` will be converted into a ```px``` amount.

## Paint

Now that the layout is calculated the elements will be drawn on the screen one by one.

There can be many multitude of layers that get painted.

## Composite

All the layers are composited into one.

