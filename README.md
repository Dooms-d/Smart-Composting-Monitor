# Smart Compost Monitor

An IoT environmental monitoring system for composting bins. An ESP32 mounted in a 3D-printed bin lid reads core temperature, headspace humidity, and ventilation state, then streams that telemetry to a live dashboard.

Originally built as a team prototype for the **Connect to Innovation** sustainability competition (Silver Achievement Standard). Now being extended into a full-stack monitoring platform.

---

## Why

Compost breaks down properly only inside a fairly narrow temperature and moisture band. Outside it, the pile goes anaerobic, stalls, or smells. This system measures those conditions continuously and drives a fan to correct temperature automatically, so the finished compost is actually usable as fertilizer — at home or at municipal scale.

---

## Architecture

```
┌─────────────────┐         ┌──────────────┐         ┌───────────────┐
│  ESP32 + sensors│  UART / │   Backend    │  HTTP   │   Dashboard   │
│  DS18B20 (temp) │  WiFi   │  Express API │ ──────> │  Chart.js UI  │
│  DHT22 (humid.) │ ──────> │  + MongoDB   │         │  live + hist. │
│  Fan (AECS)     │         │              │         │               │
└─────────────────┘         └──────────────┘         └───────────────┘
```

**Current state:** the dashboard reads telemetry directly from the ESP32 over the Web Serial API (USB/UART, 115200 baud). The backend layer is in progress.

---

## Hardware

| Component | Role |
|---|---|
| ESP32 | Microcontroller, sensor polling, telemetry output |
| DS18B20 | Core compost temperature probe |
| DHT22 | Headspace humidity and ambient temperature |
| Fan + transistor driver | Active ventilation / cooling (AECS) |
| TFT display | Local on-device readout |
| 3D-printed lid enclosure | Sensor mounting and weather protection |

---

## Telemetry format

The firmware emits one JSON object per line over serial:

```json
{"temp": 48.2, "humi": 61.5, "fan": 1}
```

| Field | Type | Meaning |
|---|---|---|
| `temp` | float | Core temperature, °C |
| `humi` | float | Headspace humidity, % |
| `fan`  | int   | Ventilation state, `0` = off, `1` = running |

---

## Repository layout

```
smart-compost-monitor/
├── dashboard/     # Web Serial + Chart.js frontend
├── firmware/      # ESP32 / Arduino sketch
├── docs/          # Diagrams, photos, demo media
└── README.md
```

---

## Running the dashboard

The Web Serial API requires a Chromium-based browser (Chrome, Edge) served over `http://localhost` or `https://`.

```bash
cd dashboard
python3 -m http.server 8000
```

Open `http://localhost:8000`, click **Connect Station**, and select the ESP32's serial port.

---

## Roadmap

- [ ] **Backend API** — Express + MongoDB endpoint receiving readings over HTTP
- [ ] **WiFi transport** — ESP32 POSTs telemetry instead of requiring a USB tether
- [ ] **Historical views** — query and chart past readings, not just the live window
- [ ] **Alert thresholds** — flag out-of-range temperature and humidity
- [ ] **Auth + reliability** — API key, WiFi reconnect and retry logic
- [ ] **Deployment** — live hosted backend and dashboard
- [ ] **Docs** — architecture diagram, setup guide, demo video

---

## Credits

Software implementation by **Shaikh Chand Muhammad Shami**. Hardware assembly was a team effort; the original concept and physical design came from the Team Emerald project.
