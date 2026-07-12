# Hand Tracker 3D

An interactive web app that lets you control glowing wireframe 3D shapes with
your hands. It uses **MediaPipe Hands** for real-time webcam hand tracking and
**Three.js (r128)** for 3D rendering — all in a single `index.html` with
vanilla JavaScript, no frameworks and no build step.

## Running

Camera access requires a secure context, so serve the file over HTTPS or
localhost (opening it via `file://` will not work in most browsers):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Allow camera access when prompted.

## Controls

| Gesture | Effect |
| --- | --- |
| One hand | Shape sticks to your hand (X/Y from hand position, Z from hand distance to the camera) |
| Tilt one hand sideways | Rolls the shape with your hand |
| Pinch thumb + index / spread fingers | Shrinks / grows the shape |
| Two hands | Shape floats at the midpoint between your hands |
| Spread / close hands | Grows / shrinks the shape |
| Raise one hand above the other | Rolls the shape (Z axis) |
| Push one hand toward the camera | Spins the shape (Y axis) |
| Tilt both hands sideways together | Pitches the shape (X axis) |
| Move fast | The shape flares and its glow intensifies |
| No hands | Shape drifts back to center with a gentle idle spin |

Your hands are drawn live on screen: a glowing skeleton in each hand's color
(cyan / pink), a soft glow in the palm, fingertip trails that fade over
1.2 seconds, and an animated energy tether flowing from each palm into the
shape — so the connection between your hands and the shape is always visible.

## Features

- Neon wireframe shapes instead of solid meshes: crisp edge lines, an additive
  halo pass, a faint translucent fill, and glowing points on every vertex,
  with a color that slowly drifts through the spectrum and reacts to how fast
  your hands move
- Full-screen mirrored webcam feed behind the 3D scene, with a camera button
  in the panel to show/hide it (tracking keeps running either way); the shape,
  skeletons, and trails are aligned to the visible video, including its edge
  cropping
- 6 selectable shapes — Cube, Sphere (geodesic), Dodecahedron, Tetrahedron,
  Octahedron, Torus Knot
- Tight, low-latency smoothing so the shape feels glued to your hands while
  still absorbing tracking jitter
- Dark theme (`#0a0e27`) with frosted-glass UI panels
- Live stats: hands detected, size, rotation, FPS
- Loading spinner while MediaPipe initializes, and a friendly error dialog if
  camera access is denied or unavailable
- Responsive layout for desktop and mobile; on mobile the app automatically
  uses the lighter tracking model and a lower pixel ratio
- Proper GPU cleanup: geometries and materials are disposed when switching
  shapes and on page unload

## Libraries (loaded from CDN)

- [Three.js r128](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)
- [@mediapipe/hands](https://www.npmjs.com/package/@mediapipe/hands) 0.4.1646424915
- [@mediapipe/camera_utils](https://www.npmjs.com/package/@mediapipe/camera_utils) 0.3.1640029074
