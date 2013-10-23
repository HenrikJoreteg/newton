# What is Newton?

Newton is an easy-to-use, feature-rich physics engine that's designed from the ground up for JavaScript.

```js

var sim = new Newton.Simulator(simulate, render, 60);
var particles = new Newton.Body();
var renderer = new Newton.Renderer(document.getElementById('viewport'));

var particleLayer = sim.createLayer();

particleLayer
  .addBody(particles)
  .addForce(new Newton.LinearGravity(Math.PI * 0.5, 0.01, 0))
  .wrapIn(new Newton.Rectangle(0, 0, 640, 480));

sim.start();

function simulate(time) {
  while (time--) {
    particles.addParticle(new Newton.Particle(Math.random() * 640, 0));
  }
}

function render(time) {
  renderer.render(sim, time);
}
```

See this
[simple demo](http://www.google.com)
in action or check out the
[Quick Start](http://www.google.com).

## The state of the art

Until Newton, the best physics libraries available for JavaScript were
[Box2d](https://github.com/kripken/box2d.js/) and
[Chipmunk](https://github.com/josephg/Chipmunk-js) -
both of which are automated ports of very capable and popular C++ projects.
Unfortunately, these ports combine the clarity and conciseness of C++ with the speed of JavaScript.
Still,
[CoffeePhysics](https://github.com/soulwire/Coffee-Physics),
[Verlet-JS](https://github.com/subprotocol/verlet-js), and
[PhysicsJS](https://github.com/wellcaffeinated/PhysicsJS)
have failed to match the clunkier but more effective C-based libraries.

## Nerdy details

### Verlet integration

Under the hood, Newton.js uses the simple and stable
[verlet method](http://www.gamedev.net/page/resources/_/technical/math-and-physics/a-verlet-based-approach-for-2d-game-physics-r2714)
to integrate Newton's equations of motion.

### Decoupled simulation

JavaScript physics engines must deal with a variety of framerates, simulation complexities,
browsers, and hardware. To deliver consistent simulations in different scenarios, Newton uses a
[render-independent fixed-time simulation step](http://gafferongames.com/game-physics/fix-your-timestep/).

The render step runs as quickly as possible via RequestAnimationFrame while the simulation runs at a separate,
fixed interval via a time accumulator. This keeps Newton smooth, fast, and stutter-free.

### Arbitrary renderer

Newton comes with a simple built-in canvas renderer for development and experimentation but allows
you to render any way you like - including Canvas, WebGL, SVG, and CSS. Newton can even run simulations
in node.js!

### Bite-sized and dependency-free

Newton is framework-and-library agnostic. It can be installed as one simple dependency or
you can pick-and-choose from its three components: Math, Physics, and Primitives.
- Math: fundamental Vector and Rectangle definitions
- Physics: adds Particles, Edges, Constraints, Forces, and the Verlet Integrator
- Primitives: building blocks like Polygons, Springs, Ropes, etc




