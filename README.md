<div align="center">

# ⛵ Yey Boats

### Open marine instrumentation for the rest of us

*A source-available stack that turns cheap ESP32 touch panels into a SignalK glass cockpit —
authored once, validated against the hardware, and rendered everywhere.*

[![License: PolyForm-NC-1.0.0](https://img.shields.io/badge/license-PolyForm--NC--1.0.0-yellow.svg)](https://polyformproject.org/licenses/noncommercial/1.0.0/)
[![SignalK](https://img.shields.io/badge/SignalK-native-1eb2a8.svg)](https://signalk.org)
[![Made for ESP32-S3](https://img.shields.io/badge/hardware-ESP32--S3-blue.svg)](#the-fleet)
![Org repos](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Forgs%2Fyey-boats&query=%24.public_repos&label=public%20repos&color=informational)

</div>

---

## The story

Marine multi-function displays are expensive, closed, and frozen: the screens are
hardcoded in firmware, so changing a layout means a new build and a trip to the
chandlery. Meanwhile a $30 ESP32-S3 touch panel has a brighter screen than a lot
of dedicated chartplotters.

**Yey Boats** started as a single firmware that rendered live [SignalK](https://signalk.org)
data on a Sunton ESP32-4848S040, and grew into a small ecosystem around one idea:

> **Describe a boat dashboard once, know it will work on the target *before* you send it,
> and render it on the instrument, in the browser, and (soon) on phones and watches.**

That idea is now four cooperating projects — a **language** for dashboards, the **firmware**
that draws them, a **manager plugin** that flashes and configures every display on the boat
from the SignalK console, and a **physics simulator** that feeds the whole thing realistic
Adriatic sailing data so none of it needs a wet boat to develop against.

---

## The fleet

| Project | What it is | Stack | Activity |
|---|---|---|---|
| 🧭 **[instruments](https://github.com/yey-boats/instruments)** | The MFD firmware. LVGL 9 glass-cockpit UI, SignalK WebSocket client, WiFi/BLE provisioning, ArduinoOTA. | C++ / Arduino / PlatformIO | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments?label=) |
| 📐 **[midl](https://github.com/yey-boats/midl)** | **M**arine **I**nstrument **D**efinition **L**anguage — declarative JSON/YAML dashboards, validated against each device's capability manifest. | TypeScript | ![last](https://img.shields.io/github/last-commit/yey-boats/midl?label=) |
| 🛠️ **[Instruments-manager](https://github.com/yey-boats/instruments-manager)** | SignalK server plugin + webapp to discover, register, configure, and OTA-update every display on the boat. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments-manager?label=) |
| 🌊 **[simulator](https://github.com/yey-boats/simulator)** | Physics-accurate Adriatic sailing simulator (Beneteau Oceanis 45) with pluggable SignalK / stdout / NMEA sinks. | Python | ![last](https://img.shields.io/github/last-commit/yey-boats/simulator?label=) |

---

## By the numbers

<div align="center">

| | Firmware | MIDL | Manager | Simulator |
|---|:---:|:---:|:---:|:---:|
| **Top language** | ![](https://img.shields.io/github/languages/top/yey-boats/instruments?label=) | ![](https://img.shields.io/github/languages/top/yey-boats/midl?label=) | ![](https://img.shields.io/github/languages/top/yey-boats/instruments-manager?label=) | ![](https://img.shields.io/github/languages/top/yey-boats/simulator?label=) |
| **Languages** | ![](https://img.shields.io/github/languages/count/yey-boats/instruments?label=) | ![](https://img.shields.io/github/languages/count/yey-boats/midl?label=) | ![](https://img.shields.io/github/languages/count/yey-boats/instruments-manager?label=) | ![](https://img.shields.io/github/languages/count/yey-boats/simulator?label=) |
| **Repo size** | ![](https://img.shields.io/github/repo-size/yey-boats/instruments?label=) | ![](https://img.shields.io/github/repo-size/yey-boats/midl?label=) | ![](https://img.shields.io/github/repo-size/yey-boats/instruments-manager?label=) | ![](https://img.shields.io/github/repo-size/yey-boats/simulator?label=) |
| **Commits / month** | ![](https://img.shields.io/github/commit-activity/m/yey-boats/instruments?label=) | ![](https://img.shields.io/github/commit-activity/m/yey-boats/midl?label=) | ![](https://img.shields.io/github/commit-activity/m/yey-boats/instruments-manager?label=) | ![](https://img.shields.io/github/commit-activity/m/yey-boats/simulator?label=) |
| **Open issues** | ![](https://img.shields.io/github/issues/yey-boats/instruments?label=) | ![](https://img.shields.io/github/issues/yey-boats/midl?label=) | ![](https://img.shields.io/github/issues/yey-boats/instruments-manager?label=) | ![](https://img.shields.io/github/issues/yey-boats/simulator?label=) |

</div>

> _All badges above are **live** — they query the GitHub API through [shields.io](https://shields.io) on every page load, so the counts, languages, and "last commit" stamps update on their own as the repos move._

Roughly **75k lines of code** across **~190 commits**, in four languages, all speaking one
protocol (SignalK) and one dashboard format (MIDL).

---

## How the pieces fit

```
        author a dashboard                  develop without a boat
        ┌──────────────┐                    ┌──────────────┐
        │     MIDL     │                    │  simulator   │  Oceanis 45 physics
        │  (the lang)  │                    │ (fake telem) │  → SignalK frames
        └──────┬───────┘                    └──────┬───────┘
               │ validate vs device                │
               │ capability manifest               ▼
               ▼                            ┌──────────────┐
        ┌──────────────┐   register / OTA   │   SignalK    │
        │   manager    │◀──────────────────▶│    server    │
        │ (SK plugin)  │   push layout      └──────┬───────┘
        └──────┬───────┘                           │ WebSocket
               │ config + firmware                 ▼
               ▼                            ┌──────────────┐
        ┌────────────────────────────────────────────────┐
        │            instruments  (ESP32-S3 firmware)     │
        │   LVGL glass-cockpit  ◀── live boat state       │
        └────────────────────────────────────────────────┘
```

---

## Getting started

- **Just want to see it?** Spin up the [simulator](https://github.com/yey-boats/simulator)
  against a local SignalK server — no hardware required.
- **Have a panel?** Flash [instruments](https://github.com/yey-boats/instruments)
  (`make build && make flash`) and provision it over WiFi/BLE.
- **Running a boat network?** Install the [manager plugin](https://github.com/yey-boats/instruments-manager)
  in SignalK to manage every display from one console.
- **Designing screens?** Read the [MIDL](https://github.com/yey-boats/midl) spec.

---

## License

Every project is **source-available under [PolyForm Noncommercial 1.0.0](https://polyformproject.org/licenses/noncommercial/1.0.0/)** —
free for personal, research, and educational use. **Commercial use requires a separate license**;
contact **rights@yey.boats**.

<div align="center">
<sub>Built by the Yey Boats Project · Fair winds ⛵</sub>
</div>
