# Hand Tracker 3D

An interactive web app that lets you control 3D shapes with your hands. It uses
**MediaPipe Hands** for real-time webcam hand tracking and **Three.js (r128)**
for 3D rendering — all in a single `index.html` with vanilla JavaScript, no
frameworks and no build step.

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
| One hand | Shape follows your hand (X/Y from hand position, Z from hand distance to the camera) |
| Two hands | Shape sits at the midpoint between your hands |
| Spread / close hands | Grows / shrinks the shape |
| Raise one hand above the other | Rolls the shape (Z axis) |
| Push one hand toward the camera | Spins the shape (Y axis) |
| Tilt both hands sideways together | Pitches the shape (X axis) |
| No hands | Shape drifts back to center with a gentle idle spin |

Fingertips (5 per hand, up to 2 hands) are drawn with glowing trails that fade
over 1.5 seconds — cyan for one hand, pink for the other.

## Features

- 5 selectable shapes — Cube, Sphere, Dodecahedron, Tetrahedron, Octahedron —
  each spawned with a random color
- Dark theme (`#0a0e27`) with frosted-glass UI panels
- Live stats: hands detected, size, rotation, FPS
- Loading spinner while MediaPipe initializes, and a friendly error dialog if
  camera access is denied or unavailable
- Responsive layout for desktop and mobile; on mobile the app automatically
  uses the lighter tracking model, lower pixel ratio, and smaller shadow maps
- Proper GPU cleanup: geometries and materials are disposed when switching
  shapes and on page unload

## Libraries (loaded from CDN)

- [Three.js r128](https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js)
- [@mediapipe/hands](https://www.npmjs.com/package/@mediapipe/hands) 0.4.1646424915
- [@mediapipe/camera_utils](https://www.npmjs.com/package/@mediapipe/camera_utils) 0.3.1640029074
