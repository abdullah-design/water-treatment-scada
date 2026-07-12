# water-treatment-scada

A SCADA/HMI simulation of a three-stage water treatment process, built on **Ignition** (Perspective module) with real-time process logic implemented in Python (Jython).

This project was built as a hands-on learning exercise to bridge my background in **Cybersecurity / Information Systems Security** with **OT (Operational Technology) systems** — an area of growing demand in critical infrastructure sectors (water, energy, oil & gas).

---

## 📋 Overview

The simulation models water flowing through three stages:

**Raw Water Tank → Treatment Tank → Clean Water Tank**

Each stage is controlled by a pump and a valve. Water only flows between stages when *both* the pump and valve for that stage are active — mirroring how real industrial process control requires multiple conditions to align before a physical process occurs.

---

## ⚙️ Features

- **Live tag-driven visualization** — tank levels update in real time via Ignition's Perspective components (Cylindrical Tanks, Pipes, Toggle Switches)
- **Automated process logic** — a Gateway Timer Script (running every 1 second) simulates realistic water flow between tanks based on pump/valve states
- **Interlocked controls** — each stage requires its pump AND valve to be active before water flows, avoiding unrealistic "instant transfer" behavior
- **Auto-refill cycle** — the system automatically restarts the cycle when tanks run dry and all controls are off, keeping the simulation demo-ready
- **Threshold-based alarm** — an alarm flag activates automatically when the Raw Water tank exceeds 90% capacity
- **Tag History** — historical logging enabled on all three tank levels for trend analysis
- **Batched read/write operations** — tag reads and writes are batched (`system.tag.readBlocking` / `writeBlocking`) rather than called individually, reducing Gateway load

---

## 🛠️ Built With

- **Ignition** (Maker Edition) — Inductive Automation's industrial automation platform
- **Perspective** — Ignition's web-based visualization module
- **Python (Jython)** — Gateway Timer Scripts for process simulation logic
- **Ignition Tag System** — Memory tags, tag history, and tag bindings

---

## 🖼️ Screenshots
<img width="1145" height="1012" alt="لقطة شاشة 2026-07-12 052734" src="https://github.com/user-attachments/assets/d5d165e5-5761-49ac-9e94-931748242125" />


---

## 🧠 What I Learned

Building this project surfaced several real-world debugging challenges typical of industrial control systems work:

- **Tag path resolution issues** caused by invisible trailing whitespace in tag names — diagnosed using Ignition's Script Console and `system.tag.browse()`
- **Race conditions in sequential calculations** — an early version of the flow logic caused water to "jump" from the first tank directly to the last, skipping the middle tank, due to reading updated values mid-calculation instead of the original tick's values. Fixed by separating read/calculate/write into distinct stages using temporary variables.
- **Binding vs. scripting separation** — learned the difference between UI-level bindings (visual state) and Gateway-level scripting (actual tag control logic), and why a component can *look* interactive without actually writing to a tag.

---

## 🚧 Known Issues / Roadmap

- [1] Time-series trend chart (Power Chart) is partially configured — pen/axis data source binding needs further debugging
- [2] Alarm system currently uses a simple boolean flag; migrating to Ignition's native Alarm Pipeline is planned
- [3] Role-based access control (Operator vs. Admin) not yet implemented — planned next step to connect this project more directly to OT security concepts
- [4] Audit logging (tracking who changed what, and when) planned as a security-focused addition

---

## 🚀 Running This Project

1. Install [Ignition](https://inductiveautomation.com/downloads) (Maker Edition license is free for non-commercial use)
2. Import the exported project file into your Ignition Gateway (`Config → Projects → Import`)
3. Open the project in Ignition Designer
4. Launch the `Main_Dashboard` view in Preview mode to interact with the simulation

---

## 📬 About Me

I'm currently completing a diploma in Information Systems Security and exploring the intersection of Cybersecurity and OT/ICS security — particularly relevant to Alberta's energy and utilities sector.

Feel free to connect if you work in OT/ICS security or have feedback on this project.

**LinkedIn:** www.linkedin.com/in/abdullah-al-hamati-62a434232



THANKS :)
