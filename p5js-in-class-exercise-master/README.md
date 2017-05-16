# p5.js in-class exercise

## Overview

This exercise uses the JavaScript library p5.js to learn about the basics of programming. p5.js is a decendant of Processing. A JavaScript framework that is designed to be easy to to use for non-programmers and designers. p5.js extends Processings core features into Javascript.

**We will cover the following:**

* p5.js basic setup
* Statments
* Variables
* Conditions

## p5.js basic setup

This exercise includes the p5.js library and index.html and empty sketch file in which we will write our code. 

Before we dive in, let's take a look at the `index.html` file. This should look quite similar to other HTML files we have worked with. 

There are two `<script>` tags near the bottom of the `<body>` tag. The first links our document to the p5.js library allowing us to use it. The second links to the `sketch.js` file. This file is where we will put our code. We will use the variables and functions in the p5.js library in our `sketch.js` file.

**Open `index.html` in a Browser or use *Live Preview* in Brackets.**

You will probably need the JavaScript console at some point to see if something when wrong. This will break the connection to *Live Preview*. You can still see changes by saving in Brackets and reloading the file in Chrome.

In p5.js like Processing. The main file you use to write your code is called a sketch. 

Our sketch is called `sketch.js`. This is what it should look like.

#### sketch.js
```javascript
//You should declare any variables here


//This function is run ONCE at the beginning
function setup() {
  
}


//This function is run CONTINUOUSLY in a loop
function draw() {
  
}

//I usually declare functions here

```

You should see two special functions. `setup()` and `draw()`. p5.js uses these functions to run our code.

#### Setup
The `setup()` function runs once, when the program first executes (after the webpage loads). This is a good place to get things *set up* and ready to run. We will declare variables here and run other code that we only need once at the beginning.

#### Draw

The `draw()` function is run over and over again. It executes anything we put inside it each time. Things like redrawing objects on the screen, checking for input (sometimes) and updating variables should be done here. 

For now we will draw something that won't change, but we will soon get a sense of how this redrawing can allow us to animate and react to user input.

## Statements

Programming at its heart is about giving the computer commands to execute. These commands are given in the form of statements. They represent a single line of executable code.

**Add the following statement inside the curly braces `{ }` of the  `draw()` function. Save and reload.**

```javascript
ellipse(50, 50, 60, 60);
```

This statment tells p5.js to draw an ellipse to the screen. You should see a very specific kind of ellipse, a circle. This function takes in four parameters which in this case are set to the values of `50`, `50`, `60` and `60`. Let look at what those parameters mean.

```javascript
ellipse(xPosition, yPosition, width, height);
```

`xPosition` is the number of pixels from the left to draw the ellipse's center.

`yPosition` is the number of pixels from the top to draw the ellipse's center.

`width` tell how wide to make it.

`height` tells how tall to make it.

Since width and height are the same we get not just an ellipse but a circle. I have given you the details of the ellipse function here but you can also read up on it in the p5.js reference [here](http://p5js.org/reference/#/p5/ellipse). 

This ellipse is being drawn on a canvas. We can see the size of the canvas if we change the background color in our sketch.

**Add the following statement inside the `setup()` function:**

```javascript
background(200);
```

You should see a grey box behind our circle now. Its pretty small. Lets make it bigger. The value '200' sets the brightness of the grey on a scale from 0 (black) to 255 (white). Read more about `background()` and how to change its color [here](http://p5js.org/reference/#/p5/background)

**Right before the `background(200);` statement add the following statement:**

```javascript
createCanvas(640, 480);
```

By default p5.js makes a tiny 100 pixel by 100 pixel canvas. This statement now makes it 640 pixels wide by 480 pixels tall. That should give us some more room to move around. After saving and reloading you should now see a much bigger box.

In addition to ellipses we can make rectangles (and squares) by using the `rect()` function.

```javascript
rect(xPosition, yPosition, width, height);
```

Unlike ellipses, rectangles start drawing from the upper left corner. [Here](http://p5js.org/reference/#/p5/rect) is the p5.js reference page for `rect()`

**Try drawing a picture with a few ellipses and rectangles.**

If you want to add color to your ellipses look up `stroke()` and `fill()` in the p5.js [reference](http://p5js.org/reference/).

## Variables

While just setting values inside the `rect()` and `ellipse()` functions works for the simple programs we have so far, using variables will make things much easier as the program gets more complicated.

Before we move on let's make sure our code looks like this:

```javascript
//You should declare any variables here


//This function is run ONCE at the beginning
function setup() {
  createCanvas( 640, 480 );
  background(200);
}


//This function is run CONTINUOUSLY in a loop
function draw() {
  ellipse(50, 50, 60, 60);
}

//I usually declare functions here

```

Lets create a variable to hold the diameter of the circle. We will want to do this in several steps.

1. Declare a new variable.
2. Assign a value.
3. Use it.

#### 1. Declare a new variable
**Add the following statement  above the `setup()` function**

```javascript
var diameter;
```

There is a good reason to declare variables outside any function that we will go into more when we talk about functions. 

#### 2. Assign a new value
**Add the following statement inside the `setup()` function**

```javascript
diameter = 50;
```

We will set the initial value of `diameter` inside the `setup()` function but later on we might change it elsewhere.

#### 3. Use it
**Replace the width and height values which are now set to `60` with the new variable `diameter` like this:**

```javascript
ellipse(50, 50, diameter, diameter);
```

This might seem like a lot of work but it means in the future if we want to change the diameter we don't have to rewrite the whole ellipse statement, we can just change the value of `diameter`.

**Create two more variables `xPosition` and `yPosition` in the same way. Give them a value of `200` each and replace the first two parameters of the ``ellipse()`` statement with `xPosition` and `yPosition` respectively.**

These three variables not only make changing values later easier, they also make it easier to understand the different parts of your code. Often simply replacing a constant value like `50` with a variable like `diameter` will help you and others understand what you are trying to do.

**Above our `ellipse()` statement but still inside the `draw()` function lets add the following statement:**

```javascript
xPosition = xPosition + 1;
```

**Before you save and reload the document, make a guess what this will do.**

Did it do what you expected? 

What the `xPosition` statement says "Take the current value of `xPosition` add one and save it back into the `xPosition` variable." So each time draw is called (which is many times a second) it is increasing the value of `xPosition` by one. As it gets greater it should move the circle farther to the right.

But why is it leaving a black streak along the page? This is because p5.js doesn't make a lot of assumptions about what you want to draw or erase. Each time it calls draw it simply draws on top of whatever it drew last time. To make the ball move without a streak move the `background(200)` statement to first line inside the `draw()` function. This should now look like a ball moving across the screen.

## Conditionals

The other thing you might notice is that once the circle hits the right edge it just keeps on going. What if we want to prevent it from going past the edge?

Lets use a conditional to solve this problem. Conditionals helps answer true or false questions by doing one thing if the statement is true and another if it is false. The main conditional we will use is an `if()` statement.

**Add the following above the "`xPosition = xPosition + 1;`" statement.**

```javascript
  if( xPosition > width ) {
    xPosition = 0;
  }
```

This `if()` statement checks to see if `xPosition > width` is true. If it does it sets the value of `xPosition` to zero. Save and reload the page.

You should see that when the circle reaches the right side it jumps back to the left side.

You are probably asking what is this new variable `width`. We haven't created a variable `width`. Like many libraries p5.js has a variety of both functions and variables built in to it that we can use. The variable `width` stores the width of the canvas. 

In our case using `width` is the same as writing `if( xPosition > 640 )`. `width` is much more useful than having to remember the current width in pixels of the canvas. Also it could potentially change and then we would have to rewrite this code. As you may guess there is also a variable called `height`.

Its a little weird right now that circle just jumps from one side to another. It might be nicer if it acted more like a ball and when it reached the edge it reversed direction as if bouncing off a wall. To do that we will create another variable.

**In the same manner that we created variables before create a new variable called `xVelocity` and assign it the value `1`. **

We are going to use this new varible `xVelocity` to replace the `1` in the statement where we increment the xPosition like this.

```javascript
xPosition = xPosition + xVelocity;
```

You can see why we called this velocity if you increase its value from one to something higher.

**Try a few different values for `xVelocity`. Try a negative number. What happens?**

Let's use this new variable to make the ball change directions at the edge. 

**Change `xPosition = 0;` to `xVelocity = -xVelocity;`. This says set xVelocity to the negative of its current value. If its current value is '1' it will change it to '-1'.**

What happens? It should work fine when we get to the right edge but after it turns around it will end up running off the left edge now. 

**Add a second if statement to check when xPosition is less than zero.**

Because the left edge is zero this should work. The statement inside the second if statement should be identical to the first. `xVelocity = -xVelocity` because if the velocity is `-1` then `--1` equals `1`.

Whenever you repeat code like this in a program you should try and see if it is really necessary to have two copies of the same code. Redunancy in a program usually means there is room for simplification.

In our case, since we want to set `xVelocity` to its negative whether it is less than zero **OR** greater than the width of the canvas, we can combine our two if statements.

**Replace the two if statements with the following**

```javascript
if( xPosition < 0 || xPosition > width ) {
  xVelocity = -xVelocity;
}
```
The to verticle slashes `||` inside the if statement stand for **"or"**. So the new statement now reads:

>"If `xPosition` is less than zero **OR** `xPosition` is greater than the width, change the direction of `xVelocity`."

That reduced six lines of code to three. Not bad.

Now that you have circle moving in the x direction (horizontally) see if you can write the code to make it work in the y direction (vertically).

**Add code for `yPosition` that mimics the behavior we have created for `xPosition`.**

If you copy the code for `xPosition` and replace `xPosition` with `yPosition` and `width` with `height` you should be able to complete this part. You will also need to create a variable `yVelocity`.

#### Bonus

**Use the `stroke()` and `fill()` functions to change the color of the circle. Can you change the color while its moving? When it hits an edge?**

**Look up the function `random()` in the p5.js [reference](http://p5js.org/reference/) and see if you can set the initial values of `xVelocity` and `yVelocity` to a random number between 1 and 10.**

**Right now the circle actually extends off the edge a little before bouncing off. Can you make it bounce when the edge of the circle reaches the edge of the canvas?**