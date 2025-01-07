
Notes on PIXI JS

- A Container is the most basic class you have. It has no graphical representation but it's used to group objects as a unit
- A Sprite is the simplest way to show a bitmap on your screen.
- Sprites can show graphics and Containers are used to group sprites to move, rotate and scale them as a whole.
- You can add containers to other containers.
- The root of everything is the Stage. The stage is the regular container the application class creates and feeds to the Renderer to render
- Anything shown on the screen must inherit from the abstract class `DisplayObject` e.g. Sprite, Container all inherit from this class
- A DisplayObject can only have one parent
- A Particle Container is a special kind of container designed to go fast.
- Graphics allows you to make primitive drawings like rectangles, circles and lines. It's useful for simple graphics without a bitmap file.
- Ticker is an object that will call a function every frame before rendering
