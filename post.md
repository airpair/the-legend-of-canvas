## Recreating a Legend

I love video games.  I love JavaScript. I wanted to learn how to put the two together.  The logical place to start was obviously recreating the greatest 8-bit Nintendo game ever, The Legend of Zelda.


## Dodongo Dislikes DOM

Not knowing anything about making videos games, I decided to jump right in. Any experienced front-end engineer can work some DOM magic, and I figured that's all I had to do. I fired up my old console and started the game.  My plan was to play the game a bunch and figure out how to emulate behavior one screen at a time.

First, I set up a viewport with the <a href="http://anonymous-function.com/zelda-canvas/images/overworld_map.png"  target="_blank">overword map</a> as the background. Each screen is 256x176 pixels, so to change the screen I just slid the background-position in CSS accordingly. I tiled up the screen into 16x16 pixel chunks and decided Link should move one quare at a time to simply movement. I made a two-dimensional array for every screen and used truthy values to represent squares Link could enter.  I made a map editor to speed up this intern-worthy process. See <a href="http://anonymous-function.com/zelda-canvas/movement.js" target="_blank">Map Editor Ouput</a>

<video preload="auto" controls style="width: 650px;">
    <source src="http://anonymous-function.com/zelda-canvas/media/mapEditor.m4v">
</video>

Next I worked on the sword cave because that's the first thing any tester or player is going to try. My objectives were:

- Print cave text typewriter-style
- Add cave sprites (like the old man)
- Interact with objects (picking up the sword)
 
<video preload="auto" controls style="width: 650px;">
    <source src="http://anonymous-function.com/zelda-canvas/media/zeldaDOM.m4v">
</video>

I was feeling pretty awesome now, but something wasn't quite right with the controls.

I was listening to arrow keypress events (or touch events on the controller) to make Link move.  It was difficult to throttle these events across browsers and devices to get a consistent movement speed. I decided to backlog these bugs and keep going.

The next thing I did was create some enemies.  Each enemy was also represented by a DOM element and I used CSS3 transitions to move them from one square to the next.
```html
//Example of Red Octorok
<div class="sprite enemy red-octorok left" style="top: 88px; left: 144px;" data-enemy="red-octorok" data-hp="1" data-damage="1" data-enemy-type="1" data-x="9" data-y="2"></div>
```
I used a similar array structure to set up <a href="http://anonymous-function.com/zelda/enemyMaps.js" target="_blank">spawn locations</a>. Most of each enemy's state was matained in the DOM, while its logic lived in the JS. Because each element moved and acted independently of another (plus the CSS transitions), collision detection proved to be a complete mess.

<video preload="auto" controls style="width: 650px;">
    <source src="http://anonymous-function.com/zelda-canvas/media/zeldaDOMEnemies.m4v">
</video>

At this point, I rage quit. The gameplay was terrible and if I didn't want to play it why would anyone else?

## Switching to Canvas

Most of my inital approach stemmed from not knowing canvas. I wanted to stay in my comfort zone but quickly realized I was going against the grain.  After an obligatory single Google search, I found Mary Rose Beth's <a href="https://vimeo.com/105955605" target="_blank">live-coding demo</a> of a simple Space Invaders clone. This presentation was a fantastic demonstration of core gameplay elements such as game loop, controls, collision detection, and most importantly, drawing to the canvas.

Her examples were easy to follow, which helped alleviate my fears. Building on these core gameplay elements, I worked on prototypes for <a href="http://anonymous-function.com/breakout/" target="_blank">Breakout</a> and <a href="http://anonymous-function.com/asteroids/" target="_blank">Asteroids</a> clones.  They were simple single-level examples, but they helped significantly with the learning experience of "How do I do 'X'"?

## Starting Over
Luckily, I didn't have to start compleletly from scratch.  My viewport and movement map still fit in the plan, and the artwork would work, I just had to split the animated GIFs into separate frames.

### Fixing Link's Movement
I kept the "tiled" structure of each screen, that still made the most sense to control where Link could and couldn't walk. He needed to be able to move freely inside a particular tile, so while his sprite is 16x16 pixels, his collision detection size is smaller. This makes it much easier to move Link around and the player doesn't need the precision of a surgeon.

### Screen Transitions
When the player goes from screen to screen, there is an awesome 1980s-esque screen wipe that happens to reveal the next area. I was able to do this easily in the game loop by ignoring controller events while the transition is happening.

<video preload="auto" controls style="width: 650px;">
    <source src="http://anonymous-function.com/zelda-canvas/media/linkMovementCanvas.m4v">
</video>

## What I Learned

I did not do enough planning to allow myself to fail fast with my first approach.  Planning was for work projects, this was just a video game.

Canvas isn't scary, it's awesome. While it was intimidating at first, once I broke from the DOM mentality things came together very quickly.

## Link to the Future
This project has been an absolute blast! I plan to keep going until Nintendo ~~hires~~ sues me.  This is still very much a work in progress, but feel free to <a href="http://anonymous-function.com/zelda-canvas/" target="_blank">try out</a> what I have so far (Desktop Chrome or iOS Chrome recommended -- don't forget to zoom) or check out the <a href="https://github.com/AnonymousFunction/anonymousfunction.github.com/tree/master/zelda-canvas" target="_blank">code on GitHub</a>.  Please keep in mind that most of what's done so far is figuring out how to solve different types of problems in the game.  When you run into problems or missing features, just blow on the cartridge...
