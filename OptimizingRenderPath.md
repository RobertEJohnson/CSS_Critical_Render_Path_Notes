# Optimizing the Render Path

## Animations 60 FPS at least.

Users can tell any FPS less than 60 FPS, which results in a poor experience.

If we take ```1s``` which is

```1000ms``` and divide it by ```60``` we get ```1000/60 = 16.6ms```

This is the number we must get under for any animation. But in reality it is even lower because the browser often must calculate additional things so just for safety we will say ```12ms``` is a good runtime for an animation.

This will ensure smooth animations to human eyes.

In reality it's unlikely that ```60fps``` will always be achieved but it should be strove for when it really matters for the user experience.

### Optimization Techniques

1. Don't overwrite yourself in CSS

In CSS everything is global scope. If you overwrite a color calculation 5 times, the browser will still compute those 5 unused times.

DRY is key, with no overwriting.

2. Write Modular CSS.

3. Selector Matching

More specific selectors require more work. This happens with nesting
```nav#header ul.sidebar li {}``` requires a lot more work than
```.list_item {}```

Browsers will parse ```RIGHT``` to ```LEFT``` with selectors so with the above specific selector it will start with all the ```li```'s then continue leftward. It takes a lot of time.

In general the browser does selector matching VERY quickly, its typically not worth rewritting your code for the additonal boost, but it can be a good thing to keep in mind that using a smaller selectors is faster.

### Paint Optimization

Go to More Tools > Rendering > enable paint flashing in the Chrome Developer Tools to get a good look at when things are being painted by the browser.

You can see the paint count by using the Layers tab under more tools in the chrome developer tools.

Click on the layer and you should be able to see a paint count.

#### Move an element to its own layer

This will help solve paint issues as well. 

The best way to tell the browser to create another layer is to use the...

```will-change:``` property with the value ```transform;```. So, ```will-change: transform;```

Most browsers react to this by putting an element on its own layer. All major browsers support this.

If needing to work with an older browser use ```transform: translateZ(0)``` This forces the browser to create a new layer.

>Promote Layers ONLY when it makes sense. 
>Let the browser manage all layers as they are costly.
>If you do promote a layer USE PROFILING to make sure it needs it.

## JavaScript vs CSS

Both work. Some Javascript animations libraries however are slow, that typically has to do with using ```setTimeout``` or ```setInterval``` for animations. DON'T do that.

Rather,
The beginning of an animation frame is THE BEST time to run JavaScript.

Use ```Request Animation Frame``` which is an API that will schedule your JS to run at the right point of every frame.
It's the only way to guarantee, that Javascript will run at the start of a frame.

By running at the start of a frame **that gives the browser as much time as possible to run other activities.**

Don't use ```setTimeout``` or ```setInterval``` for animations