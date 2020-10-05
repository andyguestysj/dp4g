---
title: Pygame - Basics
permalink: /docs/pyg-1-basics/
---

## Coordinates

Pygame uses a Cartesian coordinate system with the origin at the top left of the screen. Pygame coordinates are in the for x, y and always refer to an x offset from the left of the window and a y offset from the top of the window.

<centre>        
    <img src="{{ "/assets/img/pyg2/coords.png" | relative_url }}" alt="Cartesian coordinates system, origin top left" class="img-responsive">
</centre>

## Colours (or Colors) in Pygame

Colours in Pygame are defines in RGB format with a value of 0-255 representing the amount of red, green and blue in the colour. A fourth value in the same range can be used to change the transparency of the colour. This is known as the alpha value. The alpha value is a measure of opaqueness - a value of 0 is completely transparent, a value of 255 is completely opaque (solid).  

|Colour|RGB Values|
|---|---|
|Aqua|(  0, 255, 255)|
|Black|(  0,   0,   0)|
|Blue|(  0,  0, 255)|
|Fuchsia|(255,   0, 255)|
|Gray|(128, 128, 128)|
|Green|(  0, 128,   0)|
Lime|(  0, 255,   0)|
|Maroon|(128,  0,   0)|
|Navy Blue|(  0,  0, 128)|
|Olive|(128, 128,   0)|
|Purple|(128,  0, 128)|
|Red|(255,   0,   0)|
|Silver|(192, 192, 192)|
|Teal|(  0, 128, 128)|
|White|(255, 255, 255)|
|Yellow|(255, 255,   0)|

## Surface Objects

Surface objects are objects that represent a rectangular 2D image. The pixels of the Surface object can be changed by calling the Pygame drawing functions and then displayed on the screen. The window border, title bar, and buttons are not part of the display Surface object.

In particular, the Surface object returned by pygame.display.set_mode() is called the display Surface. Anything that is drawn on the display Surface object will be displayed on the window when the pygame.display.update() function is called. It is a lot faster to draw on a Surface object (which only exists in the computer’s memory) than it is to draw a Surface object to the computer screen. Computer memory is much faster to change than pixels on a monitor.

## Rect Objects
Pygame has two ways to represent rectangular areas (just like there are two ways to represent colors). The first is a tuple of four integers:  
1. The X coordinate of the top left corner.
2. The Y coordinate of the top left corner.
3. The width (in pixels) of the rectangle.
4. Then height (in pixels) of the rectangle.
The second way is as a pygame.Rect object, which we will call Rect objects for short. For example, the code below creates a Rect object with a top left corner at (10, 20) that is 200 pixels wide and 300 pixels tall:  
```python
import pygame
myRect = pygame.Rect(10, 20, 200, 300)
```
The handy thing about this is that the Rect object automatically calculates the coordinates for other features of the rectangle. For example, if you need to know the X coordinate of the right edge of the pygame.Rect object we stored in the myRect variable, you can just access the Rect object’s right attribute:  
```python
print(myRect.right)
```

|Attribute Name|Description|
|---|---|
|myRect.left|The int value of the X-coordinate of the left side of the rectangle.|
|myRect.right|The int value of the X-coordinate of the right side of the rectangle.|
|myRect.top|The int value of the Y-coordinate of the top side of the rectangle.|
|myRect.bottom|The int value of the Y-coordinate of the bottom side.|
|myRect.centerx|The int value of the X-coordinate of the center of the rectangle.|
|myRect.centery|The int value of the Y-coordinate of the center of the rectangle.|
|myRect.width|The int value of the width of the rectangle.|
|myRect.height|The int value of the height of the rectangle.|
|myRect.size|A tuple of two ints: (width, height)|
|myRect.topleft|A tuple of two ints: (left, top)|
|myRect.topright|A tuple of two ints: (right, top)|
|myRect.bottomleft|A tuple of two ints: (left, bottom)|
|myRect.bottomright|A tuple of two ints: (right, bottom)|
|myRect.midleft|A tuple of two ints: (left, centery)|
|myRect.midright|A tuple of two ints: (right, centery)|
|myRect.midtop|A tuple of two ints: (centerx, top)|
|myRect.midbottom|A tuple of two ints: (centerx, bottom)|

## Drawing Primitive Objects


#### Exercise 1 

1. Log in to repl.it
2. Go to [https://repl.it/@andyguest/pygDrawingPrimitives](https://repl.it/@andyguest/pygDrawingPrimitives)
3. Click on the `fork` button at the top of the window to make a copy of the code in your own repls
4. Click on the three lines at the top left of the window and then `My Repls` in the pop out menu
5. Open the `pygDrawingPrimitives` repl from your area
6. Run the code

### Looking at the code

In addition to the sections described on the previous page we have some new ones.  

The fist new section sets up some named CONSTANTS to represent colours. It is easier to remember colour names than three number colour descriptions.  
```python
# set up the colors
BLACK = (  0,   0,   0)
WHITE = (255, 255, 255)
RED = (255,   0,   0)
GREEN = (  0, 255,   0)
BLUE = (  0,   0, 255)
```
The next section draws on the surface object
```python
# draw on the surface object
DISPLAYSURF.fill(WHITE)
pygame.draw.polygon(DISPLAYSURF, GREEN, ((146, 0), (291, 106), (236, 277), (56, 277), (0, 106)))
pygame.draw.line(DISPLAYSURF, BLUE, (60, 60), (120, 60), 4)
pygame.draw.line(DISPLAYSURF, BLUE, (120, 60), (60, 120))
pygame.draw.line(DISPLAYSURF, BLUE, (60, 120), (120, 120), 4)
pygame.draw.circle(DISPLAYSURF, BLUE, (300, 50), 20, 0)
pygame.draw.ellipse(DISPLAYSURF, RED, (300, 250, 40, 80), 1)
pygame.draw.rect(DISPLAYSURF, RED, (200, 150, 100, 50))

pixObj = pygame.PixelArray(DISPLAYSURF)
pixObj[480][380] = BLACK
pixObj[482][382] = BLACK
pixObj[484][384] = BLACK
pixObj[486][386] = BLACK
pixObj[488][388] = BLACK
del pixObj
```

* **fill(color)** – The `fill()` method is not a function but a method of `pygame.Surface` objects. It will completely fill in the entire Surface object with whatever colour value you pass as for the `color` parameter.
* **pygame.draw.polygon(surface, color, pointlist, width)** – A polygon is shape made up of only flat sides. The `surface` and `color` parameters tell the function on what surface to draw the polygon, and what colour to make it.
The `pointlist` parameter is a tuple or list of points (that is, tuple or list of two-integer tuples for XY coordinates). The polygon is drawn by drawing lines between each point and the point that comes after it in the tuple. Then a line is drawn from the last point to the first point. You can also pass a list of points instead of a tuple of points.
The `width` parameter is optional. If you leave it out, the polygon that is drawn will be filled in, just like our green polygon on the screen is filled in with color. If you do pass an integer value for the `width` parameter, only the outline of the polygon will be drawn. The integer represents how many pixels `width` the polygon’s outline will be. Passing 1 for the `width` parameter will make a skinny polygon, while passing 4 or 10 or 20 will make thicker polygons. If you pass the integer 0 for the `width` parameter, the polygon will be filled in (just like if you left the `width` parameter out entirely).
All of the `pygame.draw` drawing functions have optional width parameters at the end, and they work the same way as `pygame.draw.polygon()`’s `width` parameter. Probably a better name for the `width` parameter would have been thickness, since that parameter controls how thick the lines you draw are.
* **pygame.draw.line(surface, color, start_point, end_point, width)** – This function draws a line between the `start_point` and `end_point` parameters.
* **pygame.draw.lines(surface, color, closed, pointlist, width)** – This function draws a series of lines from one point to the next, much like `pygame.draw.polygon()`. The only difference is that if you pass `False` for the closed parameter, there will not be a line from the last point in the `pointlist` parameter to the first point. If you pass `True`, then it will draw a line from the last point to the first.
* **pygame.draw.circle(surface, color, center_point, radius, width)** – This function draws a circle. The center of the circle is at the `center_point` parameter. The integer passed for the `radius` parameter sets the size of the circle.
The radius of a circle is the distance from the center to the edge. (The radius of a circle is always half of the diameter.) Passing 20 for the radius parameter will draw a circle that has a radius of 20 pixels.
* **pygame.draw.ellipse(surface, color, bounding_rectangle, width)** – This function draws an ellipse (which is like a squashed or stretched circle). This function has all the usual parameters, but in order to tell the function how large and where to draw the ellipse, you must specify the bounding rectangle of the ellipse. A **bounding rectangle** is the smallest rectangle that can be drawn around a shape. Here’s an example of an ellipse and its bounding rectangle:
<centre>        
    <img src="{{ "/assets/img/pyg2/ellipse.png" | relative_url }}" alt="Ellipse with bounding rectangle" class="img-responsive">
</centre>
The `bounding_rectangle` parameter can be a `pygame.Rect` object or a tuple of four integers. Note that you do not specify the center point for the ellipse like you do for the `pygame.draw.circle()` function.
* **pygame.draw.rect(surface, color, rectangle_tuple, width)** – This function draws a rectangle. The `rectangle_tuple` is either a tuple of four integers (for the XY coordinates of the top left corner, and the width and height) or a `pygame.Rect` object can be passed instead. If the `rectangle_tuple` has the same size for the width and height, a square will be drawn.

**pygame.PixelArray Objects**  
Unfortunately, there isn’t a single function you can call that will set a single pixel to a colour. The Pygame framework needs to run some code behind the scenes before and after drawing to a Surface object. If it had to do this for every single pixel you wanted to set, your program would run much slower.  
Instead, you should create a `pygame.PixelArray` object (we’ll call them PixelArray objects for short) of a Surface object and then set individual pixels. Creating a PixelArray object of a Surface object will “lock” the Surface object. While a Surface object is locked, the drawing functions can still be called on it, but it cannot have images like PNG or JPG images drawn on it with the `blit()` method.  
If you want to see if a Surface object is locked, the ``get_locked()`` Surface method will return `True` if it is locked and `False` if it is not.  
The PixelArray object that is returned from `pygame.PixelArray()` can have individual pixels set by accessing them with two indexes.   
To tell Pygame that you are finished drawing individual pixels, delete the PixelArray object with a `del` statement. Deleting the PixelArray object will “unlock” the Surface object so that you can once again draw images on it. If you forget to delete the PixelArray object, the next time you try to blit (that is, draw) an image to the Surface the program will raise an error that says, “pygame.error: Surfaces must not be locked during blit”.

## Drawing vs Rendering

I've referred to 'drawing to the screen' previously for simplicity's sake but now we need to start making a distinction between **drawing** and **rendering**.  

The code above describes *drawing* shapes to a surface. Doing this does not change what is on the screen directly. This changes the `surface` object in memory only. The screen does not update until we *render* it with the line `pygame.display.update`.  

Note also that we do not draw anything in the game loop in this program. We draw on the surface before the game loop starts and then simply keep rendering that same static image. The render ever repetition of the game loop means that the screen will refresh if a window is moved over our game window and then away again or our game window is resized.  

In most games we will have things on screen which change or move so they will need to be redrawn in the game loop but if our game has a single, constant background image we will only draw it once.  

## Building A Game World

Really it is best not to think about *drawing* at all. Think of it as building and updating the *game world*. Rendering is then visualising that world. When developing 3D games and using most game engines (like Unity and Unreal) it is explicitly done this way. You place objects in a location or scene and position a camera. Rendering is the process of taking the scene, calculating how to display it and sending that display information to the graphics card. (This is a simplification, modern graphic cards do much of this calculation themselves).  

If you want an analogy think of a 3D game like a stop motion animation. The characters and other objects are placed in a set and a photo is taken. The characters are then repositioned slightly and another photo is taken and so on. Each individual photo is a single render and each "game loop" another photo is taken and displayed. The series of rapidly changing images gives the illusion of movement.  

#### Exercise 2

1. Go back to your code and play around with the parameters to the drawing lines of code and see what happens.