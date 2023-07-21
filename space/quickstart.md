# A tutorial

## Starting

```js
require('space',sp)
require('logic',logic)

sp.init()
sp.start(500,{
	rel update(x,y)
		//draw
		sp.rect(10,0,50,50)
		//refresh screen
		sp.refresh()
},10)
```

Here we make use of _callbacks_. Callbacks are relations/functions that will be called by the framework itself when the program runs.

We start by initializing the library with _init_ and calling a relation _start_ with _update_ as a callback. _start_ takes a time in milliseconds and an _update_ relation. We've set _update_ to be called every 500 milliseconds.

In _update_, we use _sp.rect(10,0,50,50)_ to draw a rectangle and then refresh the screen.

See: [what is a relation?](../quickstart.html)

## Moving a Rectangle

```js
require('space',sp)

rel clear()
	sp.setRGB(255,255,255) and sp.clear()
sp.start(500,{
	rel update(x,y)
		y=x+1
		//clear
		clear()
		//draw
		sp.setRGB(0,0,0)
		sp.rect(x,0,50,50)
		sp.test(a)
		//end loop
		sp.refresh()
},10)
```

Now, we set the rectangle to move by 1 pixel each call. It's important to _clear_ the area to be drawn and then _refresh_ to get the result in the screen. We also set the RGB value of the rectangle.

The start relation takes a parameter _x_, 10, and passes it as the argument to update.

```
update(x,y)
```

Then we use the value passed to update as _x_ in _sp.rect(x,0,50,50)_ and increase it by 1 every time in _y=x+1_.

## Declarative vs Destructive

Our update relation is very declarative. It simply passes state around. The value 10 is used as the parameter _x_ which we pass to _y_, and _y_ is used as the next parameter. 

In general, a declarative language (either logic or functional) tries to keep destructive behavior to a minimum. Destructive behavior includes updating the screen.

The programmer may interpret _rect(x,0,50,50)_ as a declarative statement that "a rectangle will be drawn...". However, it's more akin to a direct command to the computer telling it to make a rectangle. Although similar, there's a subtle difference.

Either way, most of the program logic is kept declarative up to ocasionally calling the drawing interface.

## Input

Let's go a bit further and accept input. If the user presses a key, this changes the direction an image will move.

```js
...
world={x=10 and dir='right'}
img=sp.loadImage('b1.png')
sp.start(500,{	
	rel mouseup(x,y,s,s)
		print([x,y])
		//s2=s
	rel keypressed(key,s,s2)
		print(key)
		if(key='right')
			set(s,'dir',key,s2)
			true
		elseif(key='left')
			set(s,'dir',key,s2)
		elseif(key='escape')
			logic.halt()
		else
			true
			s2=s
	rel update(w,w2)
		w.x=x
		w.dir=dir
		if(dir='left')
			nx=o.x-1
		else
			nx=o.x+1
		//clear
		clear()
		//draw
		sp.setRGB(0,0,0)
		sp.drawImage(img,o.x,100)
		//end loop
		sp.refresh()
		set(o,'x',nx,o2)//!o.x=nx
		true
},world)
```

We now add other callback relations and draw an image _img_ instead of a rectangle.

The callback _keypressed(key,s,s2)_ gives the key, which we use to update the state (note that leaving it as _mouseup(x,y,s,s)_ is the same as asserting _s2=s_, i.e. not updating the state). Furthermore, the program ends if the user presses the escape key.

We use a table as the state, with _{x=10 and dir='right'}_ being the initial state.

It's important not to load the image in the _update_ relation, as it'll be called multiple times.

(Be sure to include an image _b1.png_ in the folder, of course.)

## World

A good way to represent our game world (or simulation, UI, etc.) is by using a table.

We then simply pass it to update and other callbacks.

If the user wishes for non-declarative state, they can use the _mutable_ or _Var_ libraries, though we won't cover this in this tutorial. It's then possible to hold global variables and have a more traditional loop.

## About

Cosmos and Space is open-source. If you feel like it, you can contribute to the project. It's given without any warranty.
