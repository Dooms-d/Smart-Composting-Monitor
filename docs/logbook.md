# Project Logbook — 3D Printed Smart Composting System

Design and development history from the original Team Emerald build (Connect to Innovation competition, Silver Achievement Standard).

---

## 1. Problem

Food waste is a major contributor to landfill methane emissions — roughly 30% of food produced globally goes to waste, and when it decomposes anaerobically in landfills it releases methane, a far more potent greenhouse gas than CO₂.

Composting is the obvious fix, but traditional bins fail in practice because:
- Temperature isn't monitored
- Carbon/nitrogen balance is hard to judge
- Poor aeration causes odor
- Users get no feedback on whether it's actually working

### Related UN Sustainable Development Goals
- **SDG 11** — Sustainable Cities and Communities
- **SDG 12** — Responsible Consumption and Production
- **SDG 13** — Climate Action

---

## 2. Design Goals

Efficient composting depends on maintaining:
- Temperature (target range: **45–65 °C**)
- Airflow / oxygen circulation
- Moisture control

The team researched composting microbiology, optimal temperature ranges, passive vs. active airflow systems, thermal insulation, and existing Arduino-based monitoring projects before settling on a design direction.

---

## 3. Design Evolution

| Iteration | Problem | Change | Result |
|---|---|---|---|
| **1 — Shape & geometry** | Rounded design was hard to manufacture/assemble | Switched to square modular geometry with rounded outer edges | Better printability, assembly, and internal layout |
| **2 — Airflow & odor** | Poor oxygen circulation, odor risk | Added vent holes, an internal fan, controlled airflow pathways, and an odor-filtering element near the outlet | Improved oxygen flow and odor control without sacrificing heat retention |
| **3 — Insulation** | Heat loss through chamber walls slows microbial activity | Double-wall chamber with an insulation gap and insulating material layer | More stable composting temperature |
| **4 — Electronics integration** | Internal electronics were hard to maintain and exposed to moisture | Moved to a dedicated external electronics enclosure mounted on the lid | Easier maintenance, cleaner wiring, better moisture protection |

---

## 4. Hardware

- **CAD:** designed in SolidWorks 2026 — main chamber, removable bottom tray, lid assembly, ventilation system, electronics enclosure, mounting structures
- **Fabrication:** PLA, 3D printed (chamber, tray, lid, electronics enclosure, structural supports)
- **Microcontroller:** ESP32
- **Sensors:** DS18B20 (core temperature, positioned through the lid toward the chamber center for accuracy), DHT22 (headspace humidity)
- **Display:** LCD module (I2C) in the external electronics enclosure for live local readout
- **Ventilation:** transistor-driven fan for active airflow/temperature control, plus an odor-filtering element

---

## 5. Electronics Troubleshooting

A few real integration issues came up and were resolved during development:

- **Unstable sensor readings** — traced to loose wiring and sensor-library configuration; fixed by reorganizing connections and testing pin assignments individually.
- **LCD not communicating** — wrong I2C address; fixed by identifying the correct address and correcting SDA/SCL wiring.
- **Limited enclosure space** — redesigned the electronics enclosure for better wire routing and maintenance access.
- **Intermittent power loss** — loose jumper connections; fixed by securing connections and simplifying the circuit layout.

---

## 6. Current Status

**Built and working:**
- ESP32 + DS18B20 + DHT22 sensing
- Active fan-driven ventilation with odor filtering
- Double-wall insulated 3D printed enclosure
- Local LCD readout
- Browser-based live dashboard (Chart.js) over Web Serial (USB/UART)

**Not yet built (roadmap):**
- Mobile app dashboard
- WiFi-based telemetry (backend API + database — in progress, see main README)
- Gas sensing
- AI-assisted compost analysis
- Automated temperature control loop (currently threshold-driven, not closed-loop)

---

## 7. Funding & Recognition

- Supported by seed funding covering CAD software, fabrication, electronics, and insulation testing
- Won a **Silver Achievement Standard** at the Connect to Innovation competition
- Logbook shared with the MindFuel programs team

---

## 8. Demo Media

- [Project video](https://youtu.be/2Cqe-QQN-Ig)
- [Project video](https://youtu.be/aTialcH4pKk)
