---
title: The Game Loop
permalink: /docs/pattern-3/
---

## Intent

*Decouple the progression of game time from user input and processor speed.*

## Motivation

Game loops are the quintessential example of a “game programming pattern”. Almost every game has one, no two are exactly alike, and relatively few programs outside of games use them.  

Consider early text adventure games. They waited until you entered what you wanted to do, they then updated you on the results of your actions and waited again.  

```console
YOU ARE STANDING AT THE END OF A ROAD BEFORE A SMALL BRICK
BUILDING . AROUND YOU IS A FOREST. A SMALL
STREAM FLOWS OUT OF THE BUILDING AND DOWN A GULLY.

> GO IN
YOU ARE INSIDE A BUILDING, A WELL HOUSE FOR A LARGE SPRING.
```

The code was nice and simple. Nothing happened till a command was entered. Once a command was entered the play could do nothing until that command was fully processed.  

```java
while (true)
{
  char* command = readCommand();
  handleCommand(command);
}
```

### Event Loops

Most modern software uses an approach a little more sophisticated than this. They generally sit around doing nothing until you press a key or use the mouse.  

```java
while (true)
{
  Event* event = waitForEvent();
  dispatchEvent(event);
}
```

The loop runs continuously runs, when an event happens it is handled as required. The improvement over the older systems is that events can be triggered by timers (like auto-saves) and external systems.  

Modern games are fundamentally different from most other software. Games don't (typically) sit around waiting for the player to do something. If the player goes AFK the bad guys keep moving and shooting.  

This is the first key part of the game loop - *it processes user input but doesn't wait for it*.  

```java
while (true)
{
  processInput();
  update();
  render();
}
```

`processInput()` handles any user input that has happened since the last call. Then, `update()` advances the game simulation one step. It runs AI and physics (usually in that order). Finally, `render()` draws the game so the player can see what happened.  

### Time

The game loop doesn’t pause on input. How much time does a single game loop take? In the real world it depends what the game loop is doing. In the game world we refer to a single game loop as a *tick* or a *frame* of game world time. But even this may not be fixed amount of game world time. The time taken to process a *tick* depends *how much work it has to do to calculate the update* and *the speed of the platform*.  

The other key job of the game loop is to *run the game at a consistent speed despite differences in the underlying hardware*.  

## The Pattern

A **game loop** runs continuously during gameplay. Each turn of the loop, it **processes user input** without blocking, **updates the game state**, and **renders the game**. It tracks the passage of time to **control the rate of gameplay**.  

## When To Use It

Usually this section describes when to use a pattern and when not to. Pattern over use can be a problem. However for this pattern, if you are making a game, you will use a Game Loop. The only questions are whether it is provided to you by an engine or library and whether or not you need to modify it.   

## Keep In Mind

### You may need to coordinate with the platform’s event loop

If you’re building your game on top of an OS or platform that has a graphic UI and an event loop built in, then you have two application loops in play. They’ll need to play nice together.  

Sometimes, you can take control and make your loop the only one. For example, if you’re writing a game against the venerable Windows API, your main() can just have a game loop. Inside, you can call PeekMessage() to handle and dispatch events from the OS. Unlike GetMessage(), PeekMessage() doesn’t block waiting for user input, so your game loop will keep cranking.  

Other platforms don’t let you opt out of the event loop so easily. If you’re targeting a web browser, the event loop is deeply built into browser’s execution model. There, the event loop will run the show, and you’ll use it as your game loop too. You’ll call something like requestAnimationFrame() and it will call back into your code to keep the game running.  

## Sample Code

The simplest game loop. This runs the game as fast as it can.  

```java
while (true)
{
  processInput();
  update();
  render();
}
```

Any variation in the time taken to process any part of the game loop will cause the game to speed up and slow down, likely causing stuttering.  

### Slowing the Game Loop down

If you want your game to run at a fixed rate and it is simple enough that you can guarantee that it will run at at least that rate then you can introduce a variable delay after the render to lock the game in to that rate.  

Say you want your game to run at 60 FPS. That gives you about 16 milliseconds per frame. As long as you can reliably do all of your game processing and rendering in less than that time, you can run at a steady frame rate. All you do is process the frame and then wait until it’s time for the next one, like so:  

![Game Loop With Capped Rate](/assets/img/pat1/game-loop-simple.png "Game Loop With Capped Rate")

The code looks a bit like this:  

>1000 ms / FPS = ms per frame.

```java
while (true)
{
  double start = getCurrentTime();
  processInput();
  update();
  render();

  sleep(start + MS_PER_FRAME - getCurrentTime());
}
```

The `sleep()` here makes sure the game doesn’t run too *fast* if it processes a frame quickly. It *doesn’t* help if your game runs too *slowly*. If it takes longer than 16ms to update and render the frame, your sleep time goes *negative*. If we had computers that could travel back in time, lots of things would be easier, but we don’t.  

Instead, the game slows down. You can work around this by doing less work each frame — cut down on the graphics and razzle dazzle or dumb down the AI. But that impacts the quality of gameplay for all users, even ones on fast machines.  

### Varying The Rate

Let’s try something a bit more sophisticated. The problem we have basically boils down to: 

1. Each update advances game time by a certain amount.  
2. It takes a certain amount of real time to process that.  

If step two takes longer than step one, the game slows down. If it takes more than 16 ms of processing to advance game time by 16ms, it can’t possibly keep up. But if we can advance the game by *more* than 16ms of game time in a single step, then we can update the game less frequently and still keep up.  

The idea then is to choose a time step to advance based on how much *real* time passed since the last frame. The longer the frame takes, the bigger steps the game takes. It always keeps up with real time because it will take bigger and bigger steps to get there. They call this a *variable* or *fluid* time step. It looks like:  

```java
double lastTime = getCurrentTime();
while (true)
{
  double current = getCurrentTime();
  double elapsed = current - lastTime;
  processInput();
  update(elapsed);
  render();
  lastTime = current;
}
```

Each frame, we determine how much real time passed since the last game update (`elapsed`). When we update the game state, we pass that in. The engine is then responsible for advancing the game world forward by that amount of time.  

Say you’ve got a bullet shooting across the screen. With a fixed time step, in each frame, you’ll move it according to its velocity. With a variable time step, you *scale that velocity by the elapsed time*. As the time step gets bigger, the bullet moves farther in each frame. That bullet will get across the screen in the *same* amount of *real* time whether it’s twenty small fast steps or four big slow ones. This looks like a winner:   

* The game plays at a consistent rate on different hardware.
* Players with faster machines are rewarded with smoother gameplay.

But, alas, there’s a serious problem lurking ahead: we’ve made the game non-deterministic and unstable. Here’s one example of the trap we’ve set for ourselves:  

>“Deterministic” means that every time you run the program, if you give it the same inputs, you get the exact same outputs back. As you can imagine, it’s much easier to track down bugs in deterministic programs — find the inputs that caused the bug the first time, and you can cause it every time.
>
>Computers are naturally deterministic; they follow programs mechanically. Non-determinism appears when the messy real world creeps in. For example, networking, the system clock, and thread scheduling all rely on bits of the external world outside of the program’s control.  

Say we’ve got a two-player networked game and Fred has some beast of a gaming machine while George is using his grandmother’s antique PC. That aforementioned bullet is flying across both of their screens. On Fred’s machine, the game is running super fast, so each time step is tiny. We cram, like, 50 frames in the second it takes the bullet to cross the screen. Poor George’s machine can only fit in about five frames.  

This means that on Fred’s machine, the physics engine updates the bullet’s position 50 times, but George’s only does it five times. Most games use floating point numbers, and those are subject to *rounding error*. Each time you add two floating point numbers, the answer you get back can be a bit off. Fred’s machine is doing ten times as many operations, so he’ll accumulate a bigger error than George. The *same* bullet will end up in *different places* on their machines.  

This is just one nasty problem a variable time step can cause, but there are more. In order to run in real time, game physics engines are approximations of the real laws of mechanics. To keep those approximations from blowing up, damping is applied. That damping is carefully tuned to a certain time step. Vary that, and the physics gets unstable.   

>“Blowing up” is literal here. When a physics engine flakes out, objects can get completely wrong velocities and launch themselves into the air.

This instability is bad enough that this example is only here as a cautionary tale and to lead us to something better…  

### Play Catch Up

One part of the engine that usually *isn’t* affected by a variable time step is rendering. Since the rendering engine captures an instant in time, it doesn’t care how much time advanced since the last one. It renders things wherever they happen to be right then.  

> This is more or less true. Things like motion blur can be affected by time step, but if they’re a bit off, the player doesn’t usually notice.  

We can use this fact to our advantage. We’ll *update* the game using a fixed time step because that makes everything simpler and more stable for physics and AI. But we’ll allow flexibility in when we *render* in order to free up some processor time.  

It goes like this: A certain amount of real time has elapsed since the last turn of the game loop. This is how much game time we need to simulate for the game’s “now” to catch up with the player’s. We do that using a *series* of *fixed* time steps. The code looks a bit like:  

```java
double previous = getCurrentTime();
double lag = 0.0;
while (true)
{
  double current = getCurrentTime();
  double elapsed = current - previous;
  previous = current;
  lag += elapsed;

  processInput();

  while (lag >= MS_PER_UPDATE)
  {
    update();
    lag -= MS_PER_UPDATE;
  }

  render();
}
```

There’s a few pieces here. At the beginning of each frame, we update lag based on how much real time passed. This measures how far the game’s clock is behind compared to the real world. We then have an inner loop to update the game, one fixed step at a time, until it’s caught up. Once we’re caught up, we render and start over again. You can visualize it sort of like this:  

![Game Loop With Variable Updates](/assets/img/pat1/game-loop-fixed.png "Game Loop With Variable Updates")

Note that the time step here isn’t the *visible* frame rate anymore. `MS_PER_UPDATE` is just the granularity we use to update the game. The shorter this step is, the more processing time it takes to catch up to real time. The longer it is, the choppier the gameplay is. Ideally, you want it pretty short, often faster than 60 FPS, so that the game simulates with high fidelity on fast machines.  

But be careful not to make it *too* short. You need to make sure the time step is greater than the time it takes to process an `update()`, even on the slowest hardware. Otherwise, your game simply can’t catch up.  

>I left it out here, but you can safeguard this by having the inner update loop bail after a maximum number of iterations. The game will slow down then, but that’s better than locking up completely.  

Fortunately, we’ve bought ourselves some breathing room here. The trick is that we’ve *yanked rendering out of the update loop*. That frees up a bunch of CPU time. The end result is the game *simulates* at a constant rate using safe fixed time steps across a range of hardware. It’s just that the player’s *visible window* into the game gets choppier on a slower machine.  

### Stuck In The Middle

There’s one issue we’re left with, and that’s residual lag. We update the game at a fixed time step, but we render at arbitrary points in time. This means that from the user’s perspective, the game will often display at a point in time between two updates.  

Here’s a timeline:

![Game Loop Update & Render Time Line](/assets/img/pat1/game-loop-timeline.png "Game Loop Update & Render Time Line")

As you can see, we update at a nice tight, fixed interval. Meanwhile, we render whenever we can. It’s less frequent than updating, and it isn’t steady either. Both of those are OK. The lame part is that we don’t always render right at the point of updating. Look at the third render time. It’s right between two updates:  

![Game Loop Update & Render Time Line Close Up](/assets/img/pat1/game-loop-timeline-close.png "Game Loop Update & Render Time Line Close Up")

Imagine a bullet is flying across the screen. On the first update, it’s on the left side. The second update moves it to the right side. The game is rendered at a point in time between those two updates, so the user expects to see that bullet in the center of the screen. With our current implementation, it will still be on the left side. This means motion looks jagged or stuttery.  

Conveniently, we actually know *exactly* how far between update frames we are when we render: it’s stored in `lag`. We bail out of the update loop when it’s less than the update time step, not when it’s *zero*. That leftover amount? That’s how far into the next frame we are.  

When we go to render, we’ll pass that in:  

```java
render(lag / MS_PER_UPDATE);
```

> We divide by MS_PER_UPDATE here to normalize the value. The value passed to render() will vary from 0 (right at the previous frame) to just under 1.0 (right at the next frame), regardless of the update time step. This way, the renderer doesn’t have to worry about the frame rate. It just deals in values from 0 to 1.

The renderer knows each game object and *its current velocity*. Say that bullet is 20 pixels from the left side of the screen and is moving right 400 pixels per frame. If we are halfway between frames, then we’ll end up passing 0.5 to `render()`. So it draws the bullet half a frame ahead, at 220 pixels. Ta-da, smooth motion.  

Of course, it may turn out that that extrapolation is wrong. When we calculate the next frame, we may discover the bullet hit an obstacle or slowed down or something. We rendered its position interpolated between where it was on the last frame and where we *think* it will be on the next frame. But we don’t know that until we’ve actually done the full update with physics and AI.  

So the extrapolation is a bit of a guess and sometimes ends up wrong. Fortunately, though, those kinds of corrections usually aren’t noticeable. At least, they’re less noticeable than the stuttering you get if you don’t extrapolate at all.  

## Design Decisions

### Do you own the game loop, or does the platform?
This is less a choice you make and more one that’s made for you. If you’re making a game that runs in a web browser, you pretty much can’t write your own classic game loop. The browser’s event-based nature precludes it. Likewise, if you’re using an existing game engine, you will probably rely on its game loop instead of rolling your own.  

* **Use the platform’s event loop:**
  * *It’s simple*. You don’t have to worry about writing and optimizing the core loop of the game.
  * *It plays nice with the platform*. You don’t have to worry about explicitly giving the host time to process its own events, caching events, or otherwise managing the impedance mismatch between the platform’s input model and yours.
  * *You lose control over timing*. The platform will call your code as it sees fit. If that’s not as frequently or as smoothly as you’d like, too bad. Worse, most application event loops weren’t designed with games in mind and usually are slow and choppy.

* **Use a game engine’s loop:**
  * *You don’t have to write it*. Writing a game loop can get pretty tricky. Since that core code gets executed every frame, minor bugs or performance problems can have a large impact on your game. A tight game loop is one reason to consider using an existing engine.
  * *You don’t get to write it*. Of course, the flip side to that coin is the loss of control if you do have needs that aren’t a perfect fit for the engine.

* **Write it yourself:**
  * *Total control*. You can do whatever you want with it. You can design it specifically for the needs of your game.
  * *You have to interface with the platform*. Application frameworks and operating systems usually expect to have a slice of time to process events and do other work. If you own your app’s core loop, it won’t get any. You’ll have to explicitly hand off control periodically to make sure the framework doesn’t hang or get confused.

### How do you manage power consumption?
With the advent of smartphones, laptops, and mobile gaming, the odds are good that you do care about this now. A game that runs beautifully but turns players’ phones into space heaters before running out of juice thirty minutes later is not a game that makes people happy.  

Now, you may need to think not only about making your game look great, but also use as little CPU as possible. There will likely be an upper bound to performance where you let the CPU sleep if you’ve done all the work you need to do in a frame.  

* **Run as fast as it can:**

This is what you’re likely to do for PC games (though even those are increasingly being played on laptops). Your game loop will never explicitly tell the OS to sleep. Instead, any spare cycles will be spent cranking up the FPS or graphic fidelity.  

This gives you the best possible gameplay experience but, it will use as much power as it can. If the player is on a laptop, they’ll have a nice lap warmer.  

* **Clamp the frame rate:**

Mobile games are often more focused on the quality of gameplay than they are on maximizing the detail of the graphics. Many of these games will set an upper limit on the frame rate (usually 30 or 60 FPS). If the game loop is done processing before that slice of time is spent, it will just sleep for the rest.  

This gives the player a “good enough” experience and then goes easy on their battery beyond that.  

### How do you control gameplay speed?
A game loop has two key pieces: non-blocking user input and adapting to the passage of time. Input is straightforward. The magic is in how you deal with time. There are a near-infinite number of platforms that games can run on, and any single game may run on quite a few. How it accommodates that variation is key.  

> Game-making seems to be part of human nature, because every time we’ve built a machine that can do computing, one of the first things we’ve done is made games on it. The PDP-1 was a 2 kHz machine with only 4,096 words of memory, yet Steve Russell and friends managed to create Spacewar! on it.

* **Fixed time step with no synchronization:**

This was our first sample code. You just run the game loop as fast as you can.  
* *It’s simple*. This is its main (well, only) virtue.
* *Game speed is directly affected by hardware and game complexity*. And its main vice is that if there’s any variation, it will directly affect the game speed. It’s the fixie of game loops.

* **Fixed time step with synchronization:**
The next step up on the complexity ladder is running the game at a fixed time step but adding a delay or synchronization point at the end of the loop to keep the game from running too fast.  

* *Still quite simple*. It’s only one line of code more than the probably-too-simple-to-actually-work example. In most game loops, you will likely do synchronization anyway. You will probably double buffer your graphics and synchronize the buffer flip to the refresh rate of the display.
* *It’s power-friendly*. This is a surprisingly important consideration for mobile games. You don’t want to kill the user’s battery unnecessarily. By simply sleeping for a few milliseconds instead of trying to cram ever more processing into each tick, you save power.
* *The game doesn’t play too fast*. This fixes half of the speed concerns of a fixed loop.
* *The game can play too slowly*. If it takes too long to update and render a game frame, playback will slow down. Because this style doesn’t separate updating from rendering, it’s likely to hit this sooner than more advanced options. Instead of just dropping rendering frames to catch up, gameplay will slow down.

* **Variable time step:**

I’ll put this in here as an option in the solution space with the caveat that most game developers I know recommend against it. It’s good to remember why it’s a bad idea, though.  
* *It adapts to playing both too slowly and too fast*. If the game can’t keep up with real time, it will just take larger and larger time steps until it does.
* *It makes gameplay non-deterministic and unstable*. And this is the real problem, of course. Physics and networking in particular become much harder with a variable time step.

* **Fixed update time step, variable rendering:**

The last option we covered in the sample code is the most complex, but also the most adaptable. It updates with a fixed time step, but it can drop rendering frames if it needs to to catch up to the player’s clock.  

* *It adapts to playing both too slowly and too fast*. As long as the game can update in real time, the game won’t fall behind. If the player’s machine is top-of-the-line, it will respond with a smoother gameplay experience.
* *It’s more complex*. The main downside is there is a bit more going on in the implementation. You have to tune the update time step to be both as small as possible for the high-end, while not being too slow on the low end.