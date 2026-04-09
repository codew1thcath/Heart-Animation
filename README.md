# ♥ Heart Animation — Gesture-Controlled Particle Art

A real-time, gesture-driven heart animation that runs entirely in the browser. No installs, no backend, no dependencies — just open and interact.

Built with **MediaPipe Hands** and the **Canvas API**, it tracks your hand through your webcam and responds to gestures with a particle-based heart that pulses, scales, and explodes.

---

## ✦ Demo

> Open `index.html` in Chrome or Edge, allow camera access, and use your hand.

| Gesture | Effect |
|---|---|
| 🖐️ Open hand | Heart assembles from particles |
| 🤏 Pinch (index + thumb) | Scales the heart in real time |
| ✊ Fist | Heart explodes outward |

---

## ✦ Features

- **Zero dependencies** — runs as a single `.html` file with no build step
- **Real-time hand tracking** via MediaPipe Hands (browser-native, no Python required)
- **1,200-particle heart** with glow, pulse, and physics-based explosion
- **Smooth interpolation** — scale transitions are eased, not instant
- **Directional particle explosion** — particles burst outward from the heart's center of mass
- **Ambient glow** — radial light bloom pulses with the heartbeat rhythm
- **Camera preview** — live feed visible in the corner for gesture feedback

---

## ✦ Tech Stack

| Layer | Technology |
|---|---|
| Hand Tracking | [MediaPipe Hands JS](https://google.github.io/mediapipe/solutions/hands) |
| Rendering | HTML5 Canvas API |
| Animation | `requestAnimationFrame` loop |
| Physics | Custom velocity + damping system |
| Styling | Vanilla CSS (embedded) |

---

## ✦ Getting Started

No installation required.

```bash
# Clone the repo
git clone https://github.com/your-username/heart-animation.git

# Open in browser (Chrome or Edge recommended)
open index.html
```

> ⚠️ **Use Chrome or Edge.** Firefox blocks camera access on local HTML files.  
> ⚠️ Allow camera permissions when prompted.

---

## ✦ How It Works

### Hand Detection
MediaPipe Hands processes each video frame and returns 21 hand landmarks. Finger states are derived by comparing tip landmark `y` positions against their proximal interphalangeal (PIP) joints — if the tip is above the PIP, the finger is extended.

```
Finger extended  →  landmark[tip].y < landmark[pip].y
Thumb extended   →  landmark[4].x  < landmark[3].x
```

### Gesture Logic
| Condition | Gesture |
|---|---|
| 4–5 fingers extended | `open` → spawn heart |
| 0 fingers extended | `fist` → explode |
| Index only extended | `pinch` → scale via thumb-to-index distance |

### Particle System
The heart shape is generated using the parametric equation:

```
x = 16 sin³(t)
y = 13 cos(t) − 5 cos(2t) − 2 cos(3t) − cos(4t)
```

Each of the 1,200 particles is assigned a random `t` value, placing it on the heart curve. Particles smoothly interpolate back to their origin when the heart is visible, and receive an outward velocity burst on fist detection.

---

## ✦ Project Structure

```
heart-animation/
└── index.html       # Everything — markup, styles, logic
```

---

## ✦ Browser Support

| Browser | Supported |
|---|---|
| Chrome | ✅ |
| Edge | ✅ |
| Firefox | ⚠️ Camera blocked on local files |
| Safari | ⚠️ Limited MediaPipe support |

---

## ✦ Future Ideas

- [ ] Multi-hand support (two hearts?)
- [ ] Color themes triggered by different gestures
- [ ] Sound — heartbeat audio synced to the pulse
- [ ] Mobile support via touch fallback
- [ ] Export a frame as an image

---

## ✦ Author

Made by **Cathlea Talagon**  
[GitHub](https://github.com/your-username) · [Portfolio](https://your-portfolio.com)

---

## ✦ License

MIT — free to use, modify, and share.
