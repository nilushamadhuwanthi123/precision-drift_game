# Precision Drift

An advanced endless car-racing and traffic-dodging game built with vanilla JavaScript and the Canvas API &mdash; no frameworks, no build step, no external dependencies. The road scrolls vertically toward the player across a 4-lane highway, and the goal is simple: survive as long as possible, weaving between oncoming traffic while chasing distance and pickups.

It demonstrates a fixed-timestep game-loop architecture (`requestAnimationFrame` + accumulator, with render-time position interpolation for buttery-smooth motion independent of frame rate), device-pixel-ratio-aware responsive canvas rendering, dual input handling (keyboard and touch, including swipe gestures and on-screen tap zones), accessibility considerations (`prefers-reduced-motion` support, visible focus states, live-region announcements, aria-labels), and persisted state via `localStorage`. Beyond the fundamentals, it layers in a considered difficulty curve, a two-tier pickup/power-up system, and a small object-oriented entity model (`TrafficCar`, `Pickup`, `Particle` classes) to keep the codebase organized as the simulation grows in complexity.

## Features
- Fixed-timestep game loop (accumulator pattern) decoupling physics updates from rendering, with sub-step interpolation for smooth motion at any display refresh rate
- Smooth interpolated lane changes (constant lateral speed with clamped arrival, plus a subtle steering tilt) rather than instant teleportation between lanes
- Keyboard (Arrow keys / A-D), swipe gestures, and dedicated on-screen tap controls, all routed through the same input layer
- Procedurally drawn traffic with color/size variety and independent relative-speed variation per car, spawned in "waves" that always leave at least one lane open and enforce a minimum per-lane time gap so waves never stack into an undodgeable wall
- Two-stage difficulty curve: world speed follows an asymptotic (diminishing-returns) approach to a cap so pacing intensifies early and levels off rather than spiraling; traffic density escalates in discrete distance-based tiers layered on top of the continuous speed ramp
- Two pickup types with distinct visuals and effects: coins (score bonus) and a shield power-up (temporary collision immunity with a pulsing shield ring and crash-absorb effect)
- Rectangle-overlap collision detection with shrunk hitboxes tuned for a forgiving, fair feel instead of pixel-perfect frustration
- Live HUD with running score, a speed gauge, and shield status; distinct start, pause, and game-over screens
- High score persisted via `localStorage`, shown on both the start and game-over screens with a "New Best!" indicator when beaten
- Respects `prefers-reduced-motion` by reducing particle counts and disabling screen shake, while core gameplay stays fully functional
- Auto-pause on tab/visibility change plus a manual pause overlay (Esc), and a fully DPR-aware canvas that reflows correctly on resize/orientation change mid-run
- Clean separation of concerns: config constants, entity classes, spawn/difficulty logic, collision, update, and render are each isolated into small, focused functions

## Run it
Just open `index.html` in a browser &mdash; no build step, no install.

## Live version
TBD &mdash; will be added after deployment
