# ThermAqua: Automated Waste-Heat Desalination and Fan-Cooled Condensation Cell

> **Tagline:** Waste Heat in. Fresh Water out.

---

## 📌 Project Overview
ThermAqua is an industrial energy recovery and passive desalination system that captures unharvested low-grade thermal waste (50°C to 70°C) to drive sub-boiling water purification across a vapor-permeable membrane barrier. 

Over 50% of operational energy across industrial facilities and equipment is lost as ambient heat, while plants expend up to 40% of their electricity running mechanical compressor chillers just to reject that same thermal load. ThermAqua converts this thermal dissipation into separation work: the temperature differential creates an Antoine saturation vapor pressure gradient ($\Delta P$), allowing pure water molecules to vaporize below boiling point, pass through the hydrophobic membrane interface, and leave salts, heavy minerals, and contaminants behind in the liquid chamber.

---

## ⚙️ Tech Stack & Architecture

- **Embedded Systems & Compute:** ESP32 Development Board, DS18B20 Digital Waterproof Temperature Sensor, 2-Channel 5V/12V Optocoupler Relay Module
- **Actuation & Thermal Management:** 12V DC Ceramic Heating Element (simulated thermal waste), 12V DC Brushless Convective Cooling Fan
- **Separation Science:** Direct Contact Membrane Distillation (DCMD), Microporous Hydrophobic Membrane (liquid-impermeable, vapor-permeable)
- **Thermodynamics & Computing:** Real-time Antoine Saturation Vapor Pressure ($\Delta P$) telemetry, latent heat of vaporization rejection (~2,260 kJ/kg)
- **Embedded Firmware:** C++, Arduino IDE, 1-Wire Protocol, UART Serial Telemetry (115200 baud)
- **Validation Instrumentation:** Digital TDS (Total Dissolved Solids) Meter, Non-Volatile Tracer Dye Phase Verification

---

## 🚀 Key Features
1. **Sub-Boiling Thermal Desalination:** Purifies water at 50°C–70°C, eliminating the need to consume electrical energy to reach a 100°C atmospheric boiling point.
2. **Hydrophobic Membrane Phase Separation:** Liquid water, dissolved solids, and non-volatile impurities remain strictly isolated in the feed vessel.
3. **Dual-Action Cooling & Purification:** Acts as an evaporative heat sink, dissipating latent heat of vaporization to cool the return stream while generating pure water.
4. **Autonomous Edge Loop:** The ESP32 evaluates real-time temperature gradients and dynamically drives the convective cooling fan via relay hysteresis.
5. **Zero Separation Electricity:** Operates without high-pressure reverse osmosis pumps (saving 3–6 kWh/m³), requiring only minimal parasitic power (<10W) for edge monitoring and convective airflow.
6. **Verifiable Water Purity:** Digital TDS verification confirms solute reduction from >1,000 ppm in the saline feed to <50 ppm in the collected distillate.

---

## 🔌 System Schematic & Data Flow

```text
 [ Low-Grade Waste Heat ]
       (50°C - 70°C)
             │
             ▼
┌─────────────────────────┐
│ Saline / Impure Feed    │ <─── DS18B20 Waterproof Temp Sensor
│ (Dyed High-TDS Brine)   │         │
└────────────┬────────────┘         ▼
             │                [ ESP32 Edge Controller ]
    [ Hydrophobic Membrane ]         │ (Computes Antoine ΔP)
             │                       ▼
┌────────────┴────────────┐   [ Relay Module ]
│  Condensation Chamber   │          │
│ (Active Convective Fan) │ <────────┘ (Fan Control)
└────────────┬────────────┘
             │
             ▼
  [ Pure Distilled Water ]
      (< 50 ppm TDS)
