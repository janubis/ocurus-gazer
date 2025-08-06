# Ocurus Gazer

> **Web‑camera–based 360° virtual‑tour controller**   ·   JavaScript / TypeScript · Runs fully in the browser · No server required

    

`ocurus-gazer` turns any ordinary webcam into a **hands‑free navigation device** for spherical (equirectangular) panoramas and virtual tours. It is the gaze‑tracking core we use inside [Ocurus.com](https://ocurus.com) but packaged as an open‑source micro‑library so you can drop it into **Three.js**, **A‑Frame**, React, Vue or plain JS scenes.

---

## ✨ Features

- **Zero‑setup** — import the ESM build, call `createGazer()`, that’s it.
- **MediaPipe Iris** landmarks for <2° angular error on most laptops.
- **Linear or ML gaze mapping** — start simple, switch to a CNN later without API changes.
- **Asymmetric blink detection** — right‑eye = *next*, left‑eye = *previous* scene.
- **Head‑pose panning + eye micro‑adjust** — comfortable rotation without dizziness.
- **Optional Kalman filter** for buttery‑smooth cursor.
- **No backend** — all inference runs in WebGL / WASM inside the browser.
- Written in **TypeScript**, ships with ESM/CJS/Types + declaration maps.

---

## 🚀 Quick start

```bash
# 1  Install (npm, pnpm or yarn)
npm i ocurus-gazer

# 2  Add to your TS / JS
import { createGazer } from 'ocurus-gazer';

const video = document.querySelector('#cam');
const stream = await navigator.mediaDevices.getUserMedia({ video: true });
video.srcObject = stream;
await video.play();

const gazer = await createGazer({ videoEl: video, model: 'iris', smoothing: true });

gazer.addListener(({ x, y, confidence }) => {
  // x, y ∈ [0,1]   → map to panorama camera
});
```

Need a full example? See `` for a Three.js panorama that rotates as you move your head and blinks to jump between rooms.

---

## 🛠 Folder structure

```
├─ src/            # library source (TypeScript)
│   ├─ gazer.ts    # core class
│   └─ index.ts    # tiny re‑export wrapper
├─ demo/           # standalone demo pages
├─ test/           # Vitest specs
├─ dist/           # build output (git‑ignored)
└─ docs/           # screenshots, GIFs, design notes
```

---

## 📑 API

| Function                    | Description                                                    |
| --------------------------- | -------------------------------------------------------------- |
| `createGazer(cfg)`          | Asynchronously loads the model and returns a `Gazer` instance. |
| `addListener(fn)`           | Subscribe to real‑time gaze points `{x,y,confidence,ts}`.      |
| `removeListener(fn)`        | Unsubscribe.                                                   |
| `beginCalibration(points?)` | Opens the 9‑point calibration UI (more coming soon).           |
| `pause()` / `resume()`      | Temporarily stop / continue inference.                         |
| `stop()`                    | Completely shut down and release the webcam stream.            |

See [API.md](API.md) for full type signatures and advanced options.

---

## 🧑‍💻 Development

```bash
# clone & bootstrap
git clone https://github.com/<YOUR-USER>/ocurus-gazer.git
cd ocurus-gazer && npm i

# run demo with hot reload
npm run dev

# type‑check, lint, test, bundle
npm run typecheck && npm run lint && npm run test && npm run build
```

The demo reloads instantly as you edit `src/gazer.ts`. Vitest runs in‑memory; no browsers needed.

---

## 🤝 Contributing

Pull requests are welcome ✨.  Please open an issue first if you plan a large feature so we can discuss design.  By contributing you agree to release your code under the MIT license.

### Roadmap

-

---

## 📄 License

**MIT** © 2025 Javkhlan Rentsendorj.  See [LICENSE](LICENSE) for details.

---

### Acknowledgements

Uses [MediaPipe](https://github.com/google/mediapipe) for landmark detection and was inspired by the fantastic work of WebGazer.js.

