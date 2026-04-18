# DC Motor Simulator — Physics Engine

A fully browser-based, physics-accurate DC motor simulator built as a single self-contained HTML file. No installation, no server, no API keys — just open and run.

![DC Motor Simulator](https://img.shields.io/badge/version-v5-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![HTML](https://img.shields.io/badge/built%20with-HTML%2FJS-orange)

---

## Features

- **RK4 Physics Engine** — Runge-Kutta 4th-order numerical integration of the coupled electrical and mechanical ODEs
- **2D Animated Cross-Section** — Real-time canvas-rendered motor cross-section showing rotor rotation, field lines, and current-dependent coil glow
- **3D Interactive Model** — Three.js powered 3D motor with rotating rotor, animated gear train, and drag-to-rotate / scroll-to-zoom orbit controls
- **Live Gauges** — Speed (rad/s), Current (A), Torque (N·m), Output ω, P_in, P_out, Copper Loss, and Efficiency updated every frame
- **Real-Time Charts** — Live scrolling Chart.js plots for Speed, Current, Torque, Efficiency, and Power (input vs output)
- **Gear Ratio Support** — Configurable gear reduction with animated 3D gear mesh that scales with the ratio
- **AWG Wire Calculator** — Auto-computes winding resistance from wire gauge (AWG 20–30) and coil geometry
- **Status Chips** — Stall detection, overload warning, and running state indicator
- **Efficiency Gauge** — Colour-coded arc gauge (red → amber → green) with threshold indicators
- **Motor Presets** — One-click presets for Small DC, High Torque, and Fan Load configurations
- **Toggle Physics** — Enable/disable inductance and viscous friction independently

---

## Physics Model

The simulator solves two coupled first-order ODEs:

**Electrical:**
```
V = i·R + L·(di/dt) + Kₑ·ω
```

**Mechanical:**
```
J·(dω/dt) = Kₜ·i − Bᵥ·ω − T_L
```

**Torque constant (derived from coil geometry):**
```
Kₜ = N · B · ℓ · r
```

Where `V` = supply voltage, `R` = winding resistance, `L` = inductance, `Kₑ` = back-EMF constant, `ω` = angular velocity, `J` = rotor inertia, `Bᵥ` = viscous friction, `T_L` = load torque, `N` = turns, `B` = flux density, `ℓ` = conductor length, `r` = rotor radius.

---

## Parameters

| Group | Parameters |
|---|---|
| **Electrical** | Supply Voltage (V), Winding Resistance (R), Inductance (L), Back-EMF Constant (Kₑ) |
| **Mechanical** | Rotor Inertia (J), Viscous Friction (Bᵥ), Load Torque (T_L), Gear Ratio (GR) |
| **Magnetic / Coil** | Flux Density (B), Turns (N), Conductor Length (ℓ), Rotor Radius (r) |
| **Advanced** | Simulation timestep (dt), Initial Speed (ω₀) |

---

## Usage

1. Download `dc_motor_simulator_v5.html`
2. Open it in any modern browser (Chrome, Firefox, Edge)
3. Adjust sliders or type values directly — the simulation updates live
4. Use the **Presets** panel to quickly load reference motor configurations
5. Hit **PAUSE / RESUME** to freeze the simulation, **RESET** to restart from initial conditions
6. Drag the 3D model to rotate; scroll to zoom

---

## Presets

| Preset | Description |
|---|---|
| **Small DC** | 12V hobby motor, 1.5Ω, no gear reduction |
| **High Torque** | 24V industrial-style, GR=5, heavy load |
| **Fan Load** | 18V fan, low inertia, light load |

---

## Dependencies (CDN — no install needed)

| Library | Version | Use |
|---|---|---|
| [Chart.js](https://www.chartjs.org/) | 4.4.1 | Live time-series charts |
| [Three.js](https://threejs.org/) | r128 | 3D motor model and gear rendering |
| [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) | Google Fonts | Monospace UI font |
| [Rajdhani](https://fonts.google.com/specimen/Rajdhani) | Google Fonts | Display/heading font |

All loaded from CDN. The file works offline if fonts are cached.

---

## File Structure

Everything is in one file — HTML, CSS, and JavaScript. No build step, no framework.

```
dc_motor_simulator_v5.html
├── <style>        CSS layout, theming, responsive grid
├── <body>         HTML structure (header, left panel, center panel, charts)
└── <script>
    ├── paramDefs  Parameter definitions (electrical, mechanical, magnetic, advanced)
    ├── rk4Step()  RK4 integrator (core physics)
    ├── drawMotor()        2D canvas cross-section renderer
    ├── init3D()           Three.js scene setup
    ├── rebuild3DGears()   Procedural gear mesh generator
    ├── update3D()         Per-frame 3D update
    ├── simLoop()          Main animation loop (requestAnimationFrame)
    ├── PRESETS            Motor preset configurations
    └── init()             Bootstrap
```

---

## Browser Compatibility

Works in any modern browser with WebGL support (required for the 3D view).

| Browser | Support |
|---|---|
| Chrome 90+ | ✅ |
| Firefox 88+ | ✅ |
| Edge 90+ | ✅ |
| Safari 15+ | ✅ |

---

## License

MIT — free to use, modify, and distribute.

---

## Author

Built by [Vignesh](https://github.com/vignesh23450/) as part of a browser-based engineering tools suite.
