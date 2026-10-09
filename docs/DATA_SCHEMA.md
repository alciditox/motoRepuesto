# MotoData VE - Database Schema Specification (`motoDatabase`)

This document outlines the data model and schema contracts used by MotoData VE to store motorcycle specifications, technical tuning guidelines, and cross-referenced spare parts.

---

## 🗂️ High-Level Structure

The database is structured as an in-memory JSON dictionary (`motoDatabase`) where each key represents a URL-safe model slug (e.g., `toro-rex-250`, `r3x-250`, `bera-gr`).

```typescript
interface MotoDatabase {
  [slug: string]: MotorcycleRecord;
}
```

---

## 📐 Type Definitions

### 1. `MotorcycleRecord`

| Field | Type | Description |
| :--- | :--- | :--- |
| `nombre` | `string` | Display name of the motorcycle (e.g., `"Toro Rex 250"`). |
| `marca` | `string` | Brand or commercial assembler (e.g., `"Toro Motorcycles"`). |
| `cilindrada` | `string` | Engine displacement with unit (e.g., `"250 cc"`). |
| `anio` | `string` | Production years or revision tag (e.g., `"2023 - 2024"`). |
| `optimas` | `TechnicalSpecs` | Factory operating guidelines, capacities, and tolerances. |
| `repuestos` | `SparePart[]` | Array of compatible and cross-referenced components. |

---

### 2. `TechnicalSpecs` (`optimas`)

```typescript
interface TechnicalSpecs {
  aceite: {
    tipo: string;           // Recommended oil viscosity and base (e.g. "20W-50 4T Mineral / JASO MA2")
    capacidad: string;      // Standard drain & fill volume (e.g. "1.1 L")
    conFiltro: string;      // Volume required when replacing the oil filter element (e.g. "1.2 L")
  };
  bujia: {
    codigo: string;         // OEM and standard NGK/Torch part code (e.g. "D8EA / DR8EA")
    calibracion: string;    // Electrode gap measurement (e.g. "0.60 - 0.70 mm")
  };
  frenos: {
    delantero: string;      // Caliper & rotor type, recommended fluid grade (e.g. "Disco / DOT 4")
    trasero: string;        // Rear braking mechanism (e.g. "Disco hidráulico / DOT 4")
  };
  neumaticos: {
    delantero: string;      // Tire dimensions & nominal pressure (e.g. "110/70-17")
    trasero: string;        // Tire dimensions & nominal pressure (e.g. "140/70-17")
    presionSolo: string;    // Solo rider PSI (front / rear) (e.g. "28 / 32 PSI")
    presionAcompanante: string; // Two-up / loaded rider PSI (e.g. "30 / 34 PSI")
  };
  transmision: {
    pasoCadena: string;     // Chain pitch standard (e.g. "520H")
    eslabones: string;      // Standard pitch link count (e.g. "106 eslabones")
    relacion: string;       // Front sprocket / rear sprocket tooth count (e.g. "14T / 42T")
    holgura: string;        // Vertical chain slack tolerance (e.g. "15 - 25 mm")
  };
  valvulas: {
    admision: string;       // Cold intake valve clearance tolerance (e.g. "0.05 mm")
    escape: string;         // Cold exhaust valve clearance tolerance (e.g. "0.08 mm")
  };
  bateria: {
    modelo: string;         // Standard JIS battery form-factor (e.g. "12V 9Ah (YTX9-BS)")
    dimensiones: string;    // Tray dimensions L x W x H in millimeters
  };
}
```

---

### 3. `SparePart` (`repuestos`)

```typescript
interface SparePart {
  categoria: "Motor" | "Frenos" | "Transmisión" | "Eléctrico" | "Suspensión" | "Chasis" | "Accesorios";
  pieza: string;            // Standard name of the component (e.g. "Pastillas de Freno Delanteras")
  original: string;         // Original OEM part number or brand description
  genericos: string[];      // Array of verified cross-brand and aftermarket equivalents
  dificultad: "Fácil" | "Media" | "Difícil" | "Taller"; // Installation difficulty indicator
  notas: string;            // Practical workshop notes, dimensional verification tips, fitment caveats
}
```

---

## 🛠️ Example Entry

```javascript
"bera-gr": {
  nombre: "Bera GR",
  marca: "Bera",
  cilindrada: "150 cc",
  anio: "2022+",
  optimas: {
    aceite: { tipo: "20W-50 4T Mineral JASO MA", capacidad: "1.0 L", conFiltro: "1.0 L" },
    bujia: { codigo: "D8EA (Rosca larga)", calibracion: "0.6 - 0.7 mm" },
    frenos: { delantero: "Disco hidráulico (DOT 4)", trasero: "Tambor mecánico (bandas)" },
    neumaticos: {
      delantero: "2.75-18 (28 PSI)",
      trasero: "3.00-18 (32 PSI)",
      presionSolo: "28 / 32 PSI",
      presionAcompanante: "30 / 34 PSI"
    },
    transmision: { pasoCadena: "428H", eslabones: "118", relacion: "15T / 38T", holgura: "20 - 30 mm" },
    valvulas: { admision: "0.06 mm", escape: "0.08 mm" },
    bateria: { modelo: "12V 7Ah (12N7-4A)", dimensiones: "135 x 75 x 135 mm" }
  },
  repuestos: [
    {
      categoria: "Transmisión",
      pieza: "Kit de Arrastre (Cadena, Corona y Piñón)",
      original: "Bera OEM GR150",
      genericos: ["Honda CG 125/150", "Empire Horse 150", "MD Águila 150"],
      dificultad: "Media",
      notas: "Corona de 4 orificios estándar CG. Verificar largo de tornillos de fijación."
    }
  ]
}
```
