
<div align="center">

# ⛵ Yey Boats

### Open marine instrumentation for the rest of us

*Cheap ESP32 glass-cockpit displays, a navigator you can chat with about your own boat,
and an optional box that keeps it working offline — all on [SignalK](https://signalk.org).*

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

Then the boat got connected. The **yey.boats navigator** lets you talk to your boat from
anywhere, and the **YEY box** replaces the usual Raspberry Pi + HATs with one unit that
keeps working offline.

---

## The fleet

| Project | What it is | Stack | Activity |
|---|---|---|---|
| 🧭 **[instruments](https://github.com/yey-boats/instruments)** | The MFD firmware. LVGL 9 glass-cockpit UI, SignalK WebSocket client, WiFi/BLE provisioning, ArduinoOTA. | C++ / Arduino / PlatformIO | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments?label=) |
| 📐 **[midl](https://github.com/yey-boats/midl)** | **M**arine **I**nstrument **D**efinition **L**anguage — declarative JSON/YAML dashboards, validated against each device's capability manifest. | TypeScript | ![last](https://img.shields.io/github/last-commit/yey-boats/midl?label=) |
| 🛠️ **[Instruments-manager](https://github.com/yey-boats/instruments-manager)** | SignalK server plugin + webapp to discover, register, configure, and OTA-update every display on the boat. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments-manager?label=) |
| 🌊 **[simulator](https://github.com/yey-boats/simulator)** | Physics-accurate Adriatic sailing simulator (Beneteau Oceanis 45) with pluggable SignalK / stdout / NMEA sinks. | Python | ![last](https://img.shields.io/github/last-commit/yey-boats/simulator?label=) |
| 🔗 **[signalk-yey-connector](https://github.com/yey-boats/signalk-yey-connector)** | SignalK plugin that links a boat to yey.boats: share what you choose, outbound only. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/signalk-yey-connector?label=) |

Private for now: the **navigator** (the yey.boats cloud bot), **board-imx95** (the YEY box
image), **local-llm** (the on-board model), and the open-data **locality** and **nautical
terms** packs the navigator draws on.

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

## What you get

- **Talk to your boat.** Ask *"how's the battery?"*, *"are we dragging?"* or *"who's that off the bow?"* on Telegram, the web or Claude, and get an answer from live data.
- **Know when something's wrong.** Anchor drag, bilge, battery, depth and MOB alerts go to your phone and your crew.
- **Keep it when the signal drops.** With a YEY box, the navigator runs on board on its own model.
- **Your data stays yours.** You choose what leaves the boat, and nothing on board listens for incoming connections.
- **$30 displays.** ESP32 panels show any SignalK data, laid out once in MIDL.

## From a Pi with HATs to one box

Most SignalK boats today run on a Raspberry Pi with HATs and adapters wired to the equipment. The YEY box puts all of that in one unit.

| | Raspberry Pi + HATs | YEY box |
|---|---|---|
| **Boat interfaces** | a CAN HAT, serial adapters, a GPS dongle and a separate supply | NMEA 2000/CAN, serial, GNSS, Bluetooth, LAN and boat power built in |
| **Setup** | assemble, flash, then install SignalK and plugins | power it up; SignalK, plugins and the navigator come preinstalled |
| **Without internet** | dashboards only | dashboards plus the navigator, on a local model |
| **Updates** | by hand, on an SD card | signed A/B updates with rollback |
| **yey.boats** | add the connector plugin | built in, paired with the box's own key |

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
