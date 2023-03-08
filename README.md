# Box Design

This effect is obtain using the `transform` property.

## The magic trick

We dotted the div `class="box"` with `transform: perspective() rotateY();`

```css
:root {
  --rotateDeg: 15deg;
  --perspectivePx: 750px;
}

transform: perspective(var(--perspectivePx)) rotateY(var(--rotateDeg));
```

## Step by step

### Structure

Create a div(.container) and in there put all divs(.box) what do you want into

```html
<div class="container">
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
  <div class="box"></div>
</div>
```

> This is all respectively the transform effect we looking for.
> If you want to how i create this example continue reed this part.
> If you are looking for just the CSS effect, scroll down to the "CSS" heading.

In the .box we put three divs(.sector). we use this for distribute our content in the box using `flex` and `flex-basis`

```html
<div class="box">
  <div class="sector"></div>
  <div class="sector"></div>
  <div class="sector"></div>
</div>
```

Create the content. We have a text; one number and a icon. Later use `flex-direction: row-reverse;` & `:nth-child()` to create that effect of reversing the odd boxes(.box)

```html
<div class="box">
  <div class="sector">
    established fact that a reader will be distracted by the readable conten
  </div>

  <div class="sector">02</div>

  <div class="sector">
    <span>
      <i class="fa fa-flag"></i>
    </span>
  </div>
</div>
```

### Style

First prepare our environment. Create a basic normalize for the document and let's set our .container to take up the whole screen

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Bebas Neue', cursive;
}

.container {
  background: linear-gradient(rgb(142, 92, 186), 25%, rgb(39, 26, 52));
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
```

![container_styled](https://github.com/MartinMaffei95/designs/blob/main/img/css-container.png?raw=true)

Now We define our variables, in this case we define

```css
:root {
  --rotateDeg: 15deg; /* =>> the rotation of the .box*/
  --perspectivePx: 750px; /* =>> the distance between the z plane and the user */
  --boxWidth: 70%;
  --boxHeight: 15vh;
}
```

> Perspective it's hard concept at first. Read the [MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/CSS/perspective) about that and use the propery to understand how really work

The .box general style

```css
.box {
  /* box size */
  width: var(--boxWidth);
  min-height: var(--boxHeight);
  max-height: var(--boxHeight);
  padding-inline: 4%;
  padding-block: 2%;

  /* Flex & distribut our content*/
  display: flex;
  justify-content: space-between;
  align-items: center;

  /* Color and other styles */
  background: linear-gradient(to left, #199a69, #7abfa4);
  cursor: pointer;
  overflow: hidden;
}
```

![basic_style](https://raw.githubusercontent.com/MartinMaffei95/designs/main/img/css-box-effect-one.png)

Here is the trick. Intercalate in boxes the `transform` property

```css
/* ## BOX INTERCALATED STYLE */
.box:nth-child(1n) {
  transform: perspective(var(--perspectivePx)) rotateY(var(--rotateDeg));
}
.box:nth-child(2n) {
  transform: perspective(var(--perspectivePx)) rotateY(
      calc(var(--rotateDeg) * -1)
    ); /* =>> use rotateY with inver deg for create the peaks effect */
  flex-direction: row-reverse; /* This invert our div */
}
```

![perspective_effect](https://github.com/MartinMaffei95/designs/blob/main/img/css-box-first%20effect.png?raw=true)

> This is all about effect the we looking for. The rest of the code is only for style this proyect

Now we add color!

```css
/* ## BOX COLOR  */
.box:nth-child(1) {
  z-index: 60;
  background: linear-gradient(to left, #31760e, #51d410);
}
.box:nth-child(2) {
  z-index: 50;
  background: linear-gradient(to right, #0e7676, #1ccccc);
}
.box:nth-child(3) {
  z-index: 40;
  background: linear-gradient(to left, #760e0e, #ca1717);
}
.box:nth-child(4) {
  z-index: 30;
  background: linear-gradient(to right, #676b12, #dce61e);
}
.box:nth-child(5) {
  z-index: 20;
  background: linear-gradient(to left, #891676, #e925c8);
}
.box:nth-child(6) {
  z-index: 10;
  background: linear-gradient(to right, #a2530e, #f77502);
}
```

![colors_styled_apllied](https://github.com/MartinMaffei95/designs/blob/main/img/css-box-with-color.png?raw=true)

> Put the `z-index` for create a superposition between the box and top box

We add a shadows now. First declare the variables

```css
:root {
  /* shadow effect */
  --shadowTranslateX: -5px;
  --shadowTranslateY: 15px;
  --shadowSize: 15px 1px;
  --shadowColor: #00000096;
}
```

In this step use the variables in the shadows and `z-index` of boxes to create this effect.

```css
.box:nth-child(1n) {
  box-shadow: var(--shadowTranslateX) var(--shadowTranslateY) var(--shadowSize) var(
      --shadowColor
    );
}
.box:nth-child(2n) {
  box-shadow: calc(var(--shadowTranslateX) * -1) var(--shadowTranslateY) var(
      --shadowSize
    ) var(--shadowColor);
}
```

![colors_styled_apllied](https://github.com/MartinMaffei95/designs/blob/main/img/css-box-with-shadows.png?raw=true)

Now we give some love to the items inside the boxes _( the .sector divs )_  
First the general style.

```css
.box .sector {
  padding: 2%;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

![basic_sector_style](https://github.com/MartinMaffei95/designs/blob/main/img/css-sector-basic.png?raw=true)

And give a particular style for every sector. Some important items here:  
 `flex-basis: calc(var(--boxWidth) / 2);` in Child(1 & 3): Divide space of the div between this two divs  
 `margin-inline: auto;` in Child(2):Use this for put the number in the middle of div  
 `animation` & `animation-delay` : the animations make a effect of flashing neon light.They have different `animation-delay` so that the effect is not so aggressive to the eye

```css
.box .sector:nth-child(1) {
  flex-basis: calc(var(--boxWidth) / 2);
  font-size: 1.15rem;
  color: var(--onColor);
  text-shadow: rgba(255, 255, 255, 0.568) 0px 0px 5px;
  animation: littleTwinkle 3s linear infinite;
  animation-delay: 1s;
  letter-spacing: 1px;
}
.box .sector:nth-child(2) {
  margin-inline: auto;
  font-size: 4rem;
  color: var(--onColor);
  text-shadow: var(--onColor) 0px 0px 10px;
}
.box .sector:nth-child(3) {
  flex-basis: calc(var(--boxWidth) / 2);
  font-size: 3rem;
  color: var(--onColor);
  text-shadow: rgb(255, 255, 255) 0px 0px 2px;
  animation: littleTwinkle 2s linear infinite;
  animation-delay: -1s;
}
```

![basic_sector_style](https://github.com/MartinMaffei95/designs/blob/main/img/css-sector-light-effect.png?raw=true)

### Animations

Now that the animations are explained, let's create them. For this example we create two variables more.

**FLASHING NEON LIGHT EFFECT**

```css
:root {
  /* light effect */
  --onColor: #fff;
  --offColor: rgb(197, 197, 197);
}
```

```css
/* keyframes */
@keyframes bigTwinkle {
  0% {
    text-shadow: var(--onColor) 0 0 10px;
    color: var(--onColor);
  }
  1% {
    text-shadow: var(--offColor) 0 0 00px;
    color: var(--offColor);
  }
  2%,
  40% {
    text-shadow: var(--onColor) 0 0 10px;
    color: var(--onColor);
  }
  41% {
    text-shadow: var(--offColor) 0 0 00px;
    color: var(--offColor);
  }
  42% {
    text-shadow: var(--onColor) 0 0 10px;
    color: var(--onColor);
  }
  43% {
    text-shadow: var(--offColor) 0 0 00px;
    color: var(--offColor);
  }
  44%,
  100% {
    text-shadow: var(--onColor) 0 0 10px;
    color: var(--onColor);
  }
}
@keyframes littleTwinkle {
  0% {
    text-shadow: var(--offColor) 0 0 00px;
  }
  25% {
    text-shadow: var(--offColor) 0 0 04px;
  }
  50% {
    text-shadow: var(--offColor) 0 0 10px;
  }
  75% {
    text-shadow: var(--offColor) 0 0 02px;
  }
  100% {
    text-shadow: var(--offColor) 0 0 10px;
  }
}
```

**HOVER EFFECT**
We use this effect in hover. Rotate the box and play _-again-_ the light effect

```css
/* Hover styling */

.box:hover {
  transition: transform 0.1s linear;
  transform: rotateY(var(--rotateDeg));
}

.box:hover .sector:nth-child(1) {
  animation: littleTwinkle 2s linear infinite;
  animation-delay: 1s;
}
.box:hover .sector:nth-child(3) {
  animation: littleTwinkle 1s linear infinite;
  animation-delay: 0s;
}
```

![gif](https://github.com/MartinMaffei95/designs/blob/main/img/GifMaker_20230308130127003.gif?raw=true)

### Responsive

    This part of code addapt your content to screen.

```css
/* BreakPoints */
@media (max-width: 960px) {
  /* ## TEXT ON BOX  */

  .box .sector:nth-child(1) {
    font-size: 1rem;
    letter-spacing: 0.7px;
  }
  .box .sector:nth-child(2) {
    font-size: 4rem;
  }
  .box .sector:nth-child(3) {
    font-size: 3rem;
  }
}
@media (max-width: 750px) {
  /* ## TEXT ON BOX  */

  .box .sector:nth-child(1) {
    font-size: 0.8rem;
    letter-spacing: 0.5px;
  }
  .box .sector:nth-child(2) {
    font-size: 4rem;
  }
  .box .sector:nth-child(3) {
    font-size: 3rem;
  }
}
@media (max-width: 550px) {
  /* ## TEXT ON BOX  */

  .box .sector:nth-child(1) {
    font-size: 0.7rem;
    letter-spacing: 0.7px;
  }
  .box .sector:nth-child(2) {
    font-size: 3rem;
  }
  .box .sector:nth-child(3) {
    font-size: 2.5rem;
  }
}
@media (max-width: 450px) {
  /* ## TEXT ON BOX  */

  .box .sector:nth-child(1) {
    font-size: 0.6rem;
    letter-spacing: 0.7px;
  }
  .box .sector:nth-child(2) {
    font-size: 3rem;
  }
  .box .sector:nth-child(3) {
    font-size: 2.5rem;
  }
}
```

> This is not the standard breakpoints.
