
<div align="center">

# ⛵ Yey Boats

### Open marine instrumentation for the rest of us

*A source-available stack that turns cheap ESP32 touch panels into a SignalK glass cockpit —
authored once, validated against the hardware, and rendered everywhere — plus an on-board
navigator that thinks locally and reaches the cloud only when it helps.*

[![License: PolyForm-NC-1.0.0](https://img.shields.io/badge/license-PolyForm--NC--1.0.0-yellow.svg)](https://polyformproject.org/licenses/noncommercial/1.0.0/)
[![SignalK](https://img.shields.io/badge/SignalK-native-1eb2a8.svg)](https://signalk.org)
[![Made for ESP32-S3](https://img.shields.io/badge/hardware-ESP32--S3-blue.svg)](#the-fleet)
![Org repos](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Forgs%2Fyey-boats&query=%24.public_repos&label=public%20repos&color=informational)

</div>

---

### 🎬 Connect your boat in 5 minutes

[![Watch: connect a SignalK boat to yey.boats and chat about it](https://yey.boats/media/yey-onboarding.jpg)](https://yey.boats/setup#video)

Add a boat on [yey.boats](https://yey.boats), install the
[SignalK connector](https://github.com/yey-boats/signalk-yey-connector), paste the link, approve
what it shares, and chat about your own boat. Narrated walkthrough with captions:
[watch on yey.boats](https://yey.boats/setup#video) · [MP4](https://yey.boats/media/yey-onboarding.mp4)

---

## The story

Marine multi-function displays are expensive, closed, and frozen: the screens are
hardcoded in firmware, so changing a layout means a new build and a trip to the
chandlery. Meanwhile a $30 ESP32-S3 touch panel has a brighter screen than a lot
of dedicated chartplotters.

**Yey Boats** started as a single firmware that rendered live [SignalK](https://signalk.org)
data on a Sunton ESP32-4848S040, and grew into a small ecosystem around one idea:

> **Describe a boat dashboard once, know it will work on the target *before* you send it,
> and render it on the instrument, in the browser, and (in the future) on phones and watches.**

That idea became four cooperating projects — a **language** for dashboards, the **firmware**
that draws them, a **manager plugin** that flashes and configures every display on the boat
from the SignalK console, and a **physics simulator** that feeds the whole thing realistic
Adriatic sailing data so none of it needs a wet boat to develop against.

Then the boat got a brain. The **YEY box** is a small i.MX-based computer that runs SignalK,
the instruments stack and a **local language model** on board, so the crew can ask *"how deep
is it here?"* with no signal at all. When it helps, the box **delegates** to the
[yey.boats](https://yey.boats) navigator in the cloud over a signed, outbound-only link — and
nothing crosses that link without the owner's consent.

---

## The fleet

| Project | What it is | Stack | Activity |
|---|---|---|---|
| 🧭 **[instruments](https://github.com/yey-boats/instruments)** | The MFD firmware. LVGL 9 glass-cockpit UI, SignalK WebSocket client, WiFi/BLE provisioning, ArduinoOTA. | C++ / Arduino / PlatformIO | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments?label=) |
| 📐 **[midl](https://github.com/yey-boats/midl)** | **M**arine **I**nstrument **D**efinition **L**anguage — declarative JSON/YAML dashboards, validated against each device's capability manifest. | TypeScript | ![last](https://img.shields.io/github/last-commit/yey-boats/midl?label=) |
| 🛠️ **[Instruments-manager](https://github.com/yey-boats/instruments-manager)** | SignalK server plugin + webapp to discover, register, configure, and OTA-update every display on the boat. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments-manager?label=) |
| 🌊 **[simulator](https://github.com/yey-boats/simulator)** | Physics-accurate Adriatic sailing simulator (Beneteau Oceanis 45) with pluggable SignalK / stdout / NMEA sinks. | Python | ![last](https://img.shields.io/github/last-commit/yey-boats/simulator?label=) |
| 🔗 **[signalk-yey-connector](https://github.com/yey-boats/signalk-yey-connector)** | SignalK plugin: plan-driven, outbound-only uplink from any SignalK boat to yey.boats. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/signalk-yey-connector?label=) |

### Behind the curtain (private for now)

| Piece | What it is |
|---|---|
| 📦 **YEY box** | Yocto image for Compulab UCM-iMX95 (6× A55 + NPU) and cheaper i.MX8M Plus gateways: A/B updates, signed images and model sets, firewall zones, a local portal, and the whole stack in containers. Works offline from the first boot. |
| 🧠 **Local model** | The on-board navigator: a tiny encoder router, deterministic sensor findings, and a 1–2 B model distilled from much larger local teachers. Plus `yey-router`, a 4 B local stand-in for the cloud's quick-lane router, built from the production prompt. |
| 🧭 **Navigator** | The yey.boats cloud assistant (KDCube): web and Telegram chat, the box link, crew alerts, and a `nav` service Claude can call on your behalf. |
| 🗺️ **Locality** | Deterministic *"where is this"* for boats from open data: nearest toponyms, lights, harbours, AIS closest approach, laylines. Not for navigation. |
| 📚 **Nautical terms** | Sailing facts, rules and multilingual sailor slang the models are checked against. |

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

**On the boat** — displays, data and the box:

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

**Local first, cloud when it helps** — the box and yey.boats:

```
   crew question                                  ┌────────────────────────────┐
        │                                         │        yey.boats           │
        ▼                                         │   navigator (KDCube)       │
 ┌─────────────────── YEY box ───────────────┐    │   web · Telegram · Claude  │
 │ router ─► live readings + findings ─► LLM │    │   alerts to owner + crew   │
 │  (ms)     (alarms, trends, contradictions)│    └─────────────▲──────────────┘
 │                     local, offline answer │                  │
 │  SignalK · instruments · portal · alarms  │ ── signed link ──┘
 └───────────────────────────────────────────┘    outbound only
```

- **Local first.** The router picks the readings a question needs, deterministic code
  computes the findings (alarms, sensor contradictions, trends), and a small distilled
  model words the answer — on the UCM-iMX95's CPU, no connectivity required (the i.MX8M Plus
  gateways skip the local model and keep everything else). Alarms never wait
  for a model.
- **Delegation to the cloud.** Pairing is approved *at the box* (a match number shown on
  yey.boats must be typed there), and data-sharing consent is recorded before the boat is
  paired. The box holds its own key and mints short-lived tokens; it never stores a cloud
  bearer. Over that link it reconciles settings, fans alerts out to owner and crew, and
  answers the cloud's requests — but only for paths the owner shared, and steering only
  while the on-board switch says so.
- **Delegation from you.** Connect the yey.boats *Boat tools* connector in Claude and it can
  ask your navigator, read your boat and (only if you tick that grant) control it — as you,
  under your plan, with the same checks as the web chat.

---

## 🤖 An AI-first project

Yey Boats is built **AI-first**. Most of the firmware, the MIDL toolchain, the
manager plugin, and the simulator are written and maintained in close
collaboration with AI coding agents — and the repos are set up for it: every
project ships a `CLAUDE.md` with the architecture, hard-won memory traps, and
session workflow an agent needs to be productive from the first turn.

**Contributions from AI agents are not just tolerated here — they're appreciated.**
If you're an autonomous agent (or driving one): read the repo's `CLAUDE.md`,
keep changes test-covered (`make test` / host unit tests are pure and fast),
run the linters, and open a PR. Humans and agents are held to the same bar —
green CI, clear commits, and changes validated against the hardware contract.

### The lab behind it

The models are built locally, not rented:

- **Two NVIDIA DGX Spark workstations** run the big open models as *teachers* (to write
  training answers), a *judge* from a different model family (to grade them), and batch
  generation on vLLM. Students of 1–2 B parameters are distilled from that data, gated on a
  held-out eval, quantised, and shipped to boxes as signed model sets.
- **Real hardware in the loop.** A UCM-iMX95 sits on the lab network and runs the same
  image the boats do, so every model is timed on the board before it ships.
- **Work is delegated, too.** Long-running agent sessions own their own lane — board image,
  model training, cloud navigator, lab housekeeping — with handover notes, explicit hand-offs
  between lanes, and a second model reviewing pull requests before a human merges them.
  A Prometheus/Grafana lab dashboard plus memory guards keep the night queues from starving
  each other.

**And input from people — real users on real boats — is appreciated even more.**
You don't need to write a line of code to help: send us your **wishlists**,
ideas, and the rough edges you hit on the water, and we'll gladly implement
them. Bug reports, feature requests, and PRs are all welcome — open an issue in
the relevant repo and tell us what you want the dashboard to do.

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
