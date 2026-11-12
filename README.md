
<div align="center">

# ⛵ Yey Boats

### Open marine instrumentation for the rest of us

*A source-available stack around [SignalK](https://signalk.org): cheap ESP32 glass-cockpit
displays on board, a navigator you can chat with about your own boat at
[yey.boats](https://yey.boats), and an optional YEY box that keeps it all working offline.*

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

Then the boat got connected. Any SignalK boat can now link to the **yey.boats navigator** —
ask about your boat on Telegram, the web or Claude, get alerts, and (only if you allow it)
steer the autopilot remotely. And a **YEY box** can come aboard: a small i.MX computer that
*is* the boat's SignalK server, runs the navigator locally with an **on-board language
model**, and uses the cloud only when it is reachable.

---

## The fleet

| Project | What it is | Stack | Activity |
|---|---|---|---|
| 🧭 **[instruments](https://github.com/yey-boats/instruments)** | The MFD firmware. LVGL 9 glass-cockpit UI, SignalK WebSocket client, WiFi/BLE provisioning, ArduinoOTA. | C++ / Arduino / PlatformIO | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments?label=) |
| 📐 **[midl](https://github.com/yey-boats/midl)** | **M**arine **I**nstrument **D**efinition **L**anguage — declarative JSON/YAML dashboards, validated against each device's capability manifest. | TypeScript | ![last](https://img.shields.io/github/last-commit/yey-boats/midl?label=) |
| 🛠️ **[Instruments-manager](https://github.com/yey-boats/instruments-manager)** | SignalK server plugin + webapp to discover, register, configure, and OTA-update every display on the boat. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/instruments-manager?label=) |
| 🌊 **[simulator](https://github.com/yey-boats/simulator)** | Physics-accurate Adriatic sailing simulator (Beneteau Oceanis 45) with pluggable SignalK / stdout / NMEA sinks. | Python | ![last](https://img.shields.io/github/last-commit/yey-boats/simulator?label=) |
| 🔗 **[signalk-yey-connector](https://github.com/yey-boats/signalk-yey-connector)** | SignalK plugin that links a boat to yey.boats: consent-first pairing, outbound-only uplink of the paths you share, remote requests, and a two-switch gate for remote steering. | Node.js / JavaScript | ![last](https://img.shields.io/github/last-commit/yey-boats/signalk-yey-connector?label=) |

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

## How the pieces fit

### On board: displays and SignalK

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

### Boat ↔ cloud: two ways aboard

```
   ESP32 displays ──┐                         ESP32 displays ──┐
                    ▼                                          ▼
 ┌─ your boat ────────────────┐        ┌─ YEY box (i.MX) ─────────────────────────┐
 │ SignalK server             │        │ SignalK server (CAN/N2K, GNSS, serial)   │
 │  + signalk-yey-connector   │        │  + manager + connector + BLE             │
 └──────────┬─────────────────┘        │ navigator, local copy (web /my, own bot) │
            │                          │  ├─ local: router → findings → small LLM │
            │                          │  └─ online: cloud models, signed proxy   │
            │                          │ settings + alerts link (yey.box.*)       │
            │                          └──────────┬───────────────────────────────┘
            │  outbound only, consent first       │  box-signed, outbound only
            ▼                                     ▼
 ┌─ yey.boats ──────────────────────────────────────────────────────────────────┐
 │ navigator: boats, consent, data plans, history, alerts, remote requests      │
 │ surfaces:  Telegram bot · web chat · Claude ("Boat tools" connector)         │
 └──────────────────────────────────────────────────────────────────────────────┘
```

**A SignalK boat + the connector.** Pair from yey.boats with a one-time code, tick what you
share, and the plugin opens one outbound connection — nothing listens on the boat. Only paths
in both the plan and your consent go up (a local deny list always wins), buffered through
outages. The navigator can read a shared path back on demand; writes are refused except
autopilot commands, and those need the plugin's own switch **and** a confirmed opt-in on
yey.boats, each command bound to this boat, short-lived, replay-protected and rate-limited.

**The YEY box, when you have one.** The box *is* the boat's SignalK server, with every image
on its factory partition so it boots the full stack with no internet. It runs its own copy of
the navigator for this one boat, signed in locally:

- **Online:** turns are shared between the cloud models (reached through a box-signed proxy,
  or your own API key) and the on-board model.
- **Offline:** everything is answered on board — a small router picks the readings a question
  needs, deterministic code computes alarms, trends and sensor contradictions, and a distilled
  model words the answer. Actions and a few intents always wait for the online path.
- **Linked to yey.boats:** paired to your account with its own key, the box keeps settings in
  sync and sends alarms (anchor drag, bilge, battery, MOB, depth, fire) to the owner and opted-in
  crew on Telegram. Secrets, SSH, firewall and update signing can never be set from the cloud.

**From Claude.** Connect the yey.boats *Boat tools* connector and Claude can ask your
navigator and read your boat — and control it only if you tick that separate grant — as you,
on your plan, with the same checks as the chat.

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
