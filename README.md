# MotoData VE (motoRepuesto) 🏍️🇻🇪

[![Language](https://img.shields.io/badge/Language-HTML5%20%7C%20ES6%2B%20%7C%20TailwindCSS-E34F26?style=flat-square)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![PWA Ready](https://img.shields.io/badge/PWA-Installable-5A0FC8?style=flat-square)](https://web.dev/progressive-web-apps/)
[![Platform](https://img.shields.io/badge/Platform-Mobile%20%26%20Desktop%20Web-blue?style=flat-square)](https://motodata-ve.ingenieroalcides.workers.dev/)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

> **Interactive Technical Specifications, Cross-Compatible Spare Parts Catalog & Preventive Maintenance Guide for Popular Venezuelan Motorcycles.**

Live Demo: [motodata-ve.ingenieroalcides.workers.dev](https://motodata-ve.ingenieroalcides.workers.dev/)

---

## 📖 Executive Summary

In Venezuela, motorcycle owners and repair shops frequently encounter severe friction when sourcing original equipment manufacturer (OEM) replacement parts due to localized import bottlenecks, dealer markups, and catalog fragmentation.

However, the vast majority of widely distributed motorcycle platforms in Venezuela—such as the **Toro Rex 250**, **R3X 250**, and **Bera GR**—share engine architectures, transmission splines, brake calipers, and electrical components with standardized international and generic platforms (e.g., Honda CG/CB series, Suzuki GN/EN platforms, and standardized Chinese small-displacement single-cylinder configurations).

**MotoData VE** is an offline-capable, mobile-first Progressive Web App (PWA) designed to bridge this information gap. It equips motorcyclists, fleet couriers, and professional mechanics with:
1. **Direct cross-references** between expensive/rare OEM parts and universally available generic or third-party equivalents.
2. **Factory-verified technical specifications** (fluid capacities, valve clearances, tire pressures, and spark plug tolerances).
3. **Structured preventive maintenance schedules** based on operational mileage intervals.
4. **Instant WhatsApp sharing** to request parts directly from local merchants and workshops.

---

## ⚡ Key Features

### 1. Dynamic Motorcycle Model Switcher
Seamlessly toggle between supported motorcycle models via a responsive selector. The application dynamically re-renders all specifications, compatibility cards, and recommendations with zero page reloads.

### 2. Cross-Compatible Spare Parts Engine (`#panel-repuestos`)
- **Instant Keyword Search**: Live filtering with debounced input and clear triggers.
- **Categorized Taxonomy**: Real-time filtering across critical mechanical systems:
  - ⚙️ **Engine & Drivetrain** (oil filters, clutch discs, valves, gaskets).
  - 🛑 **Braking Systems** (pads, shoes, master cylinders, brake fluids).
  - ⚡ **Electrical & Ignition** (CDI, stators, rectifiers, relays, spark plugs).
  - 🔧 **Transmission & Drive** (sprockets, chains, tensioners).
  - 🛞 **Chassis & Suspension** (fork seals, shock absorbers, bearings).
- **Direct Generic Matching**: Each component card explicitly lists OEM identifiers side-by-side with verified commercial cross-references (e.g., Honda, Yamaha, Suzuki, or standardized generic references).
- **WhatsApp Quick-Share**: Generates pre-formatted WhatsApp consultation messages so riders can send exact part specifications directly to motorcycle parts dealers with a single tap.

### 3. Optimal Technical Specifications Engine (`#panel-optimas`)
Provides verified reference metrics for workshop technicians:
- **Engine Oil**: Viscosity grade, crankcase capacity without filter, and total capacity with filter replacement.
- **Ignition**: Spark plug model designation and precision electrode gap (mm).
- **Tire Pressures**: Front and rear inflation pressures for solo riding vs. riding with passenger/cargo.
- **Drive Chain**: Standard chain pitch (e.g., 428H / 520H), link count, and recommended slack range (mm).
- **Valve Clearances**: Cold intake and exhaust valve clearance tolerances.
- **Electrical**: Battery capacity (Ah), operating voltage (12V), and terminal polarity.

### 4. Preventive Maintenance Guide (`#panel-mantenimiento`)
- Visual step-by-step procedures for oil renewal, drive chain lubrication and tension adjustment, and hydraulic brake maintenance.
- Mileage-based maintenance interval reference table (500 km break-in, 2,000 km, 5,000 km, and 10,000 km milestones).

### 5. Community-Driven Contribution Pipeline (`#aportar`)
Allows experienced mechanics and community members to submit field-tested generic part discoveries and corrections through an integrated submission form.

### 6. Progressive Web App (PWA) Capabilities
- **Native Install Banner**: Hooks into the browser's `beforeinstallprompt` event on Chromium-based Android browsers.
- **iOS Guidance Modal**: Provides step-by-step visual instructions for Safari's "Add to Home Screen" feature.
- **Offline Reliability**: Zero external runtime framework dependencies ensures fast caching and near-instant load times even in low-bandwidth or roadside conditions.

---

## 🏍️ Supported Motorcycles

| Model | Displacement | Engine Architecture | Target Segment |
| :--- | :--- | :--- | :--- |
| **Toro Rex 250** | 249 cc | Single-cylinder, 4-stroke, air/oil-cooled | Urban & Commuter Roadster |
| **R3X 250** | 249 cc | Single-cylinder, 4-stroke, counterbalanced | Dual-Sport / Adventure Touring |
| **Bera GR** | 150 / 200 cc | Single-cylinder, OHV pushrod / OHC | Utilitarian & Commercial Workhorse |

*Additional models can be added dynamically by expanding the `motoDatabase` JSON structure.*

---

## 🛠️ Architecture & Technology Stack

The application is engineered with an ultra-lightweight, zero-build-step philosophy for maximum portability and instant deployment:

```
moto_repuestos/
├── index.html            # Core SPA (HTML5 + Tailwind config + In-memory DB + UI logic)
├── .gitignore            # Git exclusion rules
├── docs/
│   ├── DATA_SCHEMA.md    # Specification for motoDatabase JSON schema
│   └── DEPLOYMENT.md     # Deployment guides for Cloudflare, GitHub Pages, Vercel
└── README.md             # Project documentation (this file)
```

- **Frontend Core**: Pure HTML5 and Vanilla ES6+ JavaScript.
- **Styling & Design System**: [Tailwind CSS](https://tailwindcss.com/) (loaded via CDN) with a tailored high-contrast dark palette:
  - Background: `asphalt` dark tones (`#070707`, `#0d0d0f`, `#131316`).
  - Accent: High-visibility `blood` racing red (`#ef4444`, `#dc2626`, `#b91c1c`).
  - Typography: `Bebas Neue` for high-impact headers and `Inter` for clean tabular data.
- **State Management**: Reactive in-memory state mapped to URL hash and DOM event listeners.

---

## 🚀 Getting Started

### Prerequisites
No special compilers, Node.js packages, or build tools are required. Any modern web browser is sufficient.

### Running Locally
1. Clone the repository:
   ```bash
   git clone https://github.com/alciditox/motoRepuesto.git
   cd motoRepuesto
   ```

2. Open `index.html` directly in your browser:
   - **Double-click** `index.html` in File Explorer, or
   - Start a lightweight HTTP server:
     ```bash
     # Using Python:
     python -m http.server 8080

     # Using Node:
     npx serve .
     ```
3. Navigate to `http://localhost:8080` in your browser.

---

## 📦 How to Add a New Motorcycle

To add a new motorcycle model, edit `index.html` and append a new entry to the `motoDatabase` object:

```javascript
"new-model-slug": {
  nombre: "Brand Model Displacement",
  marca: "Brand Name",
  cilindrada: "250 cc",
  anio: "2024+",
  optimas: {
    aceite: { tipo: "20W-50 Mineral / Semi-Sintético", capacidad: "1.1 L", conFiltro: "1.2 L" },
    bujia: { codigo: "D8EA / DR8EA", calibracion: "0.6 - 0.7 mm" },
    frenos: { delantero: "Disco hidráulico (DOT 4)", trasero: "Disco hidráulico (DOT 4)" },
    neumaticos: {
      delantero: "110/70-17 (28-30 PSI)",
      trasero: "140/70-17 (32-34 PSI)",
      presionSolo: "28 / 32 PSI",
      presionAcompanante: "30 / 34 PSI"
    },
    transmision: { pasoCadena: "520H", eslabones: "106", relacion: "14T / 42T", holgura: "15 - 25 mm" },
    valvulas: { admision: "0.05 mm", escape: "0.08 mm" },
    bateria: { modelo: "12V 9Ah (YTX9-BS)", dimensiones: "150 x 87 x 105 mm" }
  },
  repuestos: [
    {
      categoria: "Motor",
      pieza: "Filtro de Aceite",
      original: "OEM Brand Ref-01",
      genericos: ["Honda CBF 250", "Yamaha YBR 250", "Hiflo HF112"],
      dificultad: "Fácil",
      notas: "Compatible con cartuchos estándar de papel o malla metálica."
    }
  ]
}
```

For full schema documentation, consult [docs/DATA_SCHEMA.md](docs/DATA_SCHEMA.md).

---

## 🌐 Deployment Options

MotoData VE can be deployed to any static hosting provider within seconds:

- **Cloudflare Pages / Workers**: Zero-configuration static site deployment.
- **GitHub Pages**: Enabled via Settings -> Pages -> Deploy from branch (`main` / root).
- **Vercel / Netlify**: Direct drag-and-drop or Git repository connection.

See detailed instructions in [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md).

---

## 📄 License & Legal Notice

- **Software License**: Distributed under the [MIT License](LICENSE).
- **Disclaimer**: Technical data and generic cross-references are compiled from official workshop manuals and validated mechanic practices for informational purposes. Users should verify fitment and torque tolerances prior to road operation.

---

**Developed & Maintained by [Alciditox](https://github.com/alciditox)**
