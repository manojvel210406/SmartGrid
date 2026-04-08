# ⚡ SmartGrid Digital Twin — v2.0

> An industry-grade + research-grade smart grid simulation platform with AI intelligence, 3D visualization, and step-by-step learning capabilities.

---

## 🚀 Quick Start

Simply open `index.html` in any modern browser — **no build step, no server required.**

```bash
# Option 1: Direct open
open index.html

# Option 2: Local server (recommended for full feature support)
npx serve .
# or
python3 -m http.server 8080
```

---

## 🎯 Features at a Glance

### ⚡ Power System Analysis
| Feature | Method | Status |
|---------|--------|--------|
| Load Flow | Newton-Raphson (iterative) | ✅ |
| Fault Analysis | Z-Bus / Thevenin equivalent | ✅ |
| Transient Stability | Swing equation integration | ✅ |
| Economic Dispatch | Lambda iteration | ✅ |
| Y-Bus Formation | Admittance matrix | ✅ |

### 🖥 Interface Layout
```
┌─────────────────── TOP BAR (Controls) ─────────────────────┐
│  LOGO  │  Run LF  │  Fault  │  Stab  │  Dispatch  │ Status  │
├────────┼──────────────────────────────┬────────────────────┤
│        │                              │                    │
│  LEFT  │     CENTER (2D/3D Canvas)    │   RIGHT (Results)  │
│ PANEL  │                              │                    │
│        │   Interactive Digital Twin   │   Tabbed Analysis  │
│        │   + 3D Three.js View         │   Charts + Tables  │
│        │                              │                    │
├────────┴──────────────────────────────┴────────────────────┤
│    BOTTOM: Console Logs │ Step Explanation │ AI Insights    │
└─────────────────────────────────────────────────────────────┘
```

### 🎨 2D Canvas Features
- ✅ Drag-and-drop buses (snap-to-grid)
- ✅ Animated power flow particles
- ✅ Color-coded voltage status (green/yellow/red)
- ✅ Fault spark animations
- ✅ Line tripping visualization
- ✅ Zoom & pan
- ✅ Real-time voltage labels
- ✅ Loading % on each line

### 🌐 3D Visualization (Three.js)
- ✅ Glowing bus spheres (height = voltage deviation)
- ✅ Animated tube lines with particles
- ✅ Vertical voltage pillars
- ✅ Generator cylinders
- ✅ Orbit controls (drag to rotate, scroll to zoom)
- ✅ Fog depth effect
- ✅ Fault pulse animations
- ✅ Background star field
- ✅ Grid floor

### 🧠 Intelligence Layer
- ✅ AI Engineering Assistant panel
- ✅ "Fix My System" auto-suggestions
- ✅ Explainable results (What / Why / How to Fix)
- ✅ Voltage collapse detection
- ✅ Thermal overload warnings
- ✅ Loss analysis insights

### 🎮 Advanced Features
- ✅ Scenario Timeline (t=0→3, Normal→Fault→Trip→Recovery)
- ✅ Disturbance Control Panel (sliders)
- ✅ Challenge Mode (gamified grid fixing)
- ✅ Demo Mode (auto-loads IEEE 5-Bus)
- ✅ Beginner / Advanced / Research modes
- ✅ Step-by-step equation display (Learn Mode)
- ✅ Full Analysis Pipeline (auto-run all modules)

---

## 📐 Power System Theory

### Newton-Raphson Load Flow
The load flow solves the nonlinear power balance equations:

```
P_i = Σ_j V_i · V_j · (G_ij·cos(θ_ij) + B_ij·sin(θ_ij))
Q_i = Σ_j V_i · V_j · (G_ij·sin(θ_ij) - B_ij·cos(θ_ij))
```

Solved iteratively until |ΔP, ΔQ| < ε (default: 1×10⁻⁶)

### Y-Bus Formation
```
Y_ii = Σ y_ik + jb_shunt     (diagonal: self admittance)
Y_ij = -y_ij                  (off-diagonal: mutual admittance)
```

### Fault Current (3-Phase)
```
I_f = V_prefault / (Z_ff + Z_f)
```
Where Z_ff is the driving point impedance at fault bus.

### Swing Equation (Stability)
```
2H/ωs · d²δ/dt² = Pm - Pe - D·dδ/dt
```

### Economic Dispatch (λ-iteration)
```
dC_i/dP_i = λ  (equal incremental cost condition)
P_i = (λ - b_i) / (2·a_i)
```

---

## 🏗 Architecture

```
smartgrid/
│
├── index.html          ← Complete single-file application
│   ├── CSS Styles      ← Custom design system (dark futuristic)
│   ├── PowerEngine     ← Math calculation module
│   │   ├── buildYBus()
│   │   ├── newtonRaphson()
│   │   ├── faultAnalysis()
│   │   ├── stabilityAnalysis()
│   │   └── economicDispatch()
│   ├── React Components
│   │   ├── App            ← Main orchestrator
│   │   ├── GridCanvas     ← 2D canvas rendering
│   │   ├── ThreeView      ← 3D Three.js scene
│   │   ├── LeftPanel      ← Bus/Line builder
│   │   ├── LoadFlowTab    ← Load flow results
│   │   ├── FaultTab       ← Fault analysis results
│   │   ├── StabilityTab   ← Stability charts
│   │   ├── AnalyticsTab   ← Line loading heatmap
│   │   ├── DispatchTab    ← Economic dispatch
│   │   └── BottomPanel    ← Logs + Steps + Insights
│   └── Three.js Scene
│       ├── Buses → Glowing spheres
│       ├── Lines → Animated tubes
│       ├── Generators → Cylinders
│       └── Particles → Flow indicators
│
├── README.md           ← This file
└── docs/
    ├── THEORY.md       ← Power system theory
    └── API.md          ← Component interfaces
```

---

## 🖱 Usage Guide

### Building a System
1. Click **"Load IEEE 5-Bus"** for a prebuilt demo, or
2. Use **Left Panel → Add Bus** to add buses one by one
3. Select bus **type**: Slack (reference), PV (generator), PQ (load)
4. Add **lines** connecting buses with R, X, B parameters
5. Toggle lines to **trip** circuit breakers

### Running Analysis
1. **⚡ Load Flow** — Solve for bus voltages and line flows
2. **⚠ Fault** — Select a bus, then run fault analysis
3. **〜 Stability** — Check transient stability (swing equation)
4. **$ Dispatch** — Optimal economic dispatch

### Timeline Scrubber
Drag the timeline slider at the bottom of the canvas:
- **t=0** Normal operation
- **t=1** Apply fault
- **t=2** Breaker trip
- **t=3** System recovery

### 3D View
Click the **3D** toggle (top-right of canvas) to switch to Three.js view:
- Drag to orbit
- Scroll to zoom
- Bus height = voltage deviation from nominal

---

## 🎓 Educational Features

### Beginner Mode
- Step-by-step Y-Bus formation shown
- Equation derivations in bottom panel
- Plain-language explanations of every result

### Advanced Mode
- Full Newton-Raphson iteration log
- Per-unit conversion details
- Jacobian mismatch tracking

### Research Mode
- Raw numerical data
- Convergence metrics
- Parameter sensitivity hints

---

## 📊 Prebuilt Systems

| System | Buses | Lines | Type |
|--------|-------|-------|------|
| IEEE 3-Bus | 3 | 3 | Simple tutorial |
| IEEE 5-Bus | 5 | 6 | Standard benchmark |
| Custom | Any | Any | User-defined |

---

## 🔌 Dependencies (CDN — no install needed)

| Library | Version | Purpose |
|---------|---------|---------|
| React | 18.2.0 | UI framework |
| ReactDOM | 18.2.0 | DOM rendering |
| Babel Standalone | 7.23.5 | JSX transpilation |
| Chart.js | 4.4.1 | 2D charts |
| Three.js | r128 | 3D visualization |
| Google Fonts | — | Orbitron, Rajdhani, Share Tech Mono |

---

## 🔧 Extending the System

### Adding a New Calculation Module
```javascript
// In PowerEngine object:
myNewAnalysis(buses, lines, params) {
  // Your calculation here
  return { result, steps, insights };
}
```

### Adding a New Bus Type
Add to the bus type dropdown and handle in `buildYBus()`.

### Adding Real-Time Data
Replace static bus parameters with WebSocket or REST API polling:
```javascript
useEffect(() => {
  const ws = new WebSocket('ws://your-scada-system/live');
  ws.onmessage = (e) => setBuses(JSON.parse(e.data));
}, []);
```

---

## 🏆 Design Philosophy

This simulator was built to feel like:
> "A real-time power grid digital twin operating from a cinematic control room — where every number tells a story and every calculation comes with an explanation."

The UI uses a **retro-futuristic dark theme** with:
- **Orbitron** font for labels and headings (sci-fi engineering)
- **Rajdhani** for body text (clean military/industrial)
- **Share Tech Mono** for numerical data (monospaced precision)
- Deep blue/void backgrounds with cyan/green glow accents
- CSS scanline overlay for CRT authenticity
- Animated power flow particles on all lines

---

## 📜 License

MIT License — Free to use, modify, and distribute.

---

*Built with ⚡ for power engineers, educators, and researchers.*
