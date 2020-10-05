---
title: Pygame - Introduction
permalink: /docs/pyg-0-intro/
---

This module is focused on the game development process and its useful to illustrate this by, well, going through the process, and that means making a game or two along the way. So we're going to have a look at using Pygame to make games. Pygame is a games library for the Python programming language.  

This module isn't a **programming** module as such. You won't be assessed on your coding or even your code design. I'm not expecting you to learn a whole new language (Python) when you are still being taught the first one (Java). I'll provide you with games as a starting point, provide you with code to work from and to use. You might need to extend it a little but I'm happy to explain how to do that.   

I want to show you how things work in games and Python with Pygame gives me a way to do this. Ideally I'd like to use a Game Engine but getting that installed, setup and supported on computers you can use is very difficult under the current situation. So we'll use Pygame and see what we can do!  

## Pygame On repl.it

Repl.it, the browser based code compiler, supports Pygame. If you haven't already [signed up for a repl.it account](repl.it) please do so now.  

Once you've registered you can log in. Then go to [https://repl.it/@andyguest/pygHelloWorld](https://repl.it/@andyguest/pygHelloWorld) and click on the `Fork` button at the top of the screen. Then click on the three lines icon at the top left of the screen and select `My repls` from the pop out menu. From their click on `pygHelloWorld` to open your copy of my Pygame HelloWorld programme. Run it by clicking on the green triangle button at the top of the screen. (I recommend going in to the settings by using the cog icon on the left of the screen and change the Layout to Stacked).  

Impressive huh? Okay, it's kinda pathetic, it opens up a window. It sets the title to "Hello World!". That's about it. Click the stop button at the top of the screen (with the square on it) to end the 'game'.    Or you can click on the X at the top right of the game window.  

Lets have a look at the code.

## Hello World Code

As basic as this code is, it uses many of the core concepts needed by all Pygames. Lets work our way through the code and see what's there.

### Library Importing

If we want to use a games library the first thing we need to do is import it.  

```python
import pygame, sys
from pygame.locals import *
```
The first line `import pygame` imports the core of the Pygame library. Don't worry about `sys` for now, that is a library that provided system specific information. The `import pygame` line doesn't import all of Pygame, it would be unusual to use all of Pygame so we will only import what we need. The second line `from pygame.locals import *` imports a specific part of the Pygame library. `pygame.locals` gives us easy access to constants we'll be using.  

### Initialise Pygame
```python
pygame.init()
```
The first thing we need to do is to initialise Pygame. `pygame.init()` does an the standard initialisation required for all Pygame games. It should basically be the first line of code after the imports of every Pygame.  

### Window Setup

```python
DISPLAYSURF = pygame.display.set_mode((400, 300))
pygame.display.set_caption('Hello World!')
```
These two lines set up the game window.  
`DISPLAYSURF = pygame.display.set_mode((400, 300))` creates a game window of 400x300 pixels.  
`pygame.display.set_caption('Hello World!')` sets the caption in the window title bar to "Hello World!".  

### The Game Loop
```python
while True: # main game loop
```
This single line encapsulates one of the biggest concepts in games programming, the game loop.  
<centre>        
    <img src="{{ "/assets/img/pyg2/gameloop.png" | relative_url }}" alt="Game loop cycle - input, update, render" class="img-responsive">
</centre>

Most games are based around a game loop. After the game is initialised it enters a loop. It remains in that loop until the game is completed. Three different processes are carried out each time the loop is repeated, the order can vary but it is usually  
1. Handle Events
  * Any input from the user, key presses, controller use, mouse use, etc, are processed. These may change the game state directly or may queue up actions to be taken during **2. Update Game State**. Events to be handled may also consist of time based triggers or external events in server or multiplayer games.
2. Update Game State
  * The game state is updated based on any events detected in the first stage (unless directly updated there), game physics, game AI, etc. During this stage objects are moved, collisions are detected and appropriate re/actions are taken. Objects might be moved back so they stop when they collide, damage or explosions to one or both objects might happen.
3. Draw Screen
  * Once all the updates to the game state are completed the screen is updated to show new information, positions, etc.

The Game Loop is useful for a number of reasons.  
* By collating the effects of events without updating the game state we can carry out the updates in an efficient and effective manner.
* By turning events in to actions to be processed, and treating the game updates as actions to be processed we can maintain a history of actions allowing us to roll back time if we need to.
* It is possible to treat player characters as objects driven by input and non-player characters as objects driven by AI control. If the difference between them is limited to how they are controlled then a lot of code becomes reusable.

The biggest advantage to the Game Loop is the ability to control the speed of the game consistently. 

In gaming we have two separate times that we care about. There is the real world time, how long it takes to update the code, redraw the screen, etc. and there is the game time, how much time has passed in the game.

The Game Loop timing is where these meet. Every time we complete a game loop repetition an amount of time in the game state/world passes. It takes a real world time-span to complete one repetition of the game loop and that time-span isn't fixed.

The time taken to *handle events* varies depending on the number of events but since the event is used to create an action the time taken to handle events doesn't vary by much. *Updating the game state* is far more unpredictable. The actions can vary, some are quick to update, others are slow. *Drawing the screen* can vary a great deal too, especially for 3D games with special effects (which is most of them!). *Drawing the screen* is typically the part of the game loop that takes the longest.

If we say that one repetition of a game loop represents a single fixed step in time of the game world then if the time taken to complete the repetition varies our game is going to stutter as some updates happen quickly and others slowly.

There are a number of solutions to this. We won't go in to detail here but it is possible to 
* add a delay/pause to the game loop if it updates to quickly - effectively setting a limit on how fast the game can be updated.
* if our game loop is running slowly one option is to carry out step two - updating the game state - enough times to catch up before drawing the screen. Since the draw is the slowest part of the loop we get chance to catch up. The game will visually update at a varying rate but the movement on screen should be consistent
* another option is to tell the update how much time has passed since the last update and have the update change the state by a varying amount rather than a fixed rate.  

Depending on the game, and the hardware it will be running on, one of these techniques can help smooth the gameplay out.

### Event Handling

The first stage of the game loop is the handling of events. We typically think of this as input events from the player but it could be time or other external triggers.  

```python
  for event in pygame.event.get():  # process input

    if event.type == QUIT:
      pygame.quit()
      sys.exit()

```
Pygame keeps a list of events that have happened. `for event in pygame.event.get():` will loop through each event in turn. Within this loop `event` refers to the event currently being processed.  

`if event.type == QUIT:` checks to see if the event is a `QUIT` event, from clicking on the X at the top right of the game window. If the event was triggered by a key being pressed down the `event.type` would be `KEYDOWN` or `KEYUP` when the button was released. The event could be soemthing like `MOUSEMOTION`, `MOUSEBUTTONUP`, `VIDEORESIZE` or a number of other events. 

For key presses we'd also need to identify which key was pressed.  
```python
  for event in pygame.event.get():  # process input

    if event.type == KEYDOWN:
      if event.key == K_w: # key is K(eyboard)_w( key)
        move_forward()
```

The only event handled in our "Hello World!" game is the QUIT event. This causes pygame to be shut down and the the code to be exited.

### Update Game State

Our little "Hello World!" game is completely static so there is no game state update.

### Draw The Screen - Rendering
```python
pygame.display.update() # render - update the display
```
Here we update the screen. We aren't doing anything clever in the rendering since we aren't doing anything clever on screen so the render call is nice and simple.

