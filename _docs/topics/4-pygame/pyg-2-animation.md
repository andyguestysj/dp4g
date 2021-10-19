---
title: Pygame - Animation
permalink: /docs/pyg-2-animation/
---

We've seen how images can be drawn to surfaces and rendered to the screen so how do we animate our displays? How do we make things move?  

To understand this lets go back to the analogy of stop motion animation. In stop motion animation a scene is created with objects and characters and a photo is taken. Next the scene is updated, characters are moved very slightly, and then another photo is taken. The characters are moved a little more and another photo is taken. The process repeats until enough photos are taken to turn in to a video of the scene. It is a long, laborious process.

Fortunately for us we can get the computer to do the majority of the work and produce animation much faster, but the principle is the same, we make small changes in every game loop repetition.  



Not the most exciting animation in the world but it is a start!  

Much of the code looks the same as before but we have some additions

### Frames Per Second

```python
FPS = 30 # frames per second setting
fpsClock = pygame.time.Clock()
#
#
while True: # Game Loop
    #
    pygame.display.update()
    fpsClock.tick(FPS) # Standardising the game loop time
```

These parts of the code standardise the game loop update rate to 30 frames per second, ensuring that our game runs at a fixed rate, providing we don't take too long processing each game loop repetition. In this case the contents of the game loop are so simple out game would run too fast. This code slows it down to a fixed 30 FPS.  

### Initialisation of a simple sprite

```python
pilotImg = pygame.image.load('pilot.jpg')
positionX , positionY = 100, 200
velocityX, velocityY = 5, 0
```

Here we set up our little pilot. we load a jpg image to use as a sprite and we set the pilots position and velocity.  
Note that python lets us assign multiple values in this way `positionX, positionY = 100, 200` sets positionX to 100 and positionY to 200.  

### Game State Update

```python
  # Update Game State
  positionX = positionX + velocityX
  positionY = positionY + velocityY

  if positionX > 350 or positionX < 50:
    velocityX = velocityX * -1
```
Here we update the pilots position by adding on its velocity. We then check to see if the pilot has moved as far to the left or right as we will allow and if it has we reverse its direction.  

### Rendering

```python
  # Render Screen
  DISPLAYSURF.fill(WHITE)
  DISPLAYSURF.blit(pilotImg,(positionX,positionY))
  pygame.display.update()
  fpsClock.tick(FPS) # Standardising the game loop time
```

Here we render the screen. We need to clear the screen to white every time because the scene has changed and we want to remove what was previously visible. We then `blit` the jpeg image of the pilot at the current position. Finally we render the scene to the screen.





