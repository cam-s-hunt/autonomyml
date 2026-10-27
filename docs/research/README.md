# AutonomyML Architecture Research

This directory collects architectural research, comparative standards analyses, and schema prototypes supporting the design of the **Autonomy Model Language (AutonomyML)** specification.

## Research Documents

| Document | Focus | Relevance to [AutonomyML Overview](../../AutonomyML%20Overview.md) |
| :--- | :--- | :--- |
| [Reference Runtime & Module Boundaries](./reference-runtime-module-boundaries.md) | Architectural separation between the **AutonomyML Mission Executive (`autonomyml-app`)** and **OGC CS API Servers (`semconnect`, OpenSensorHub)**, showing how `autonomyml-app` is built as an independent application on the **`semengine` Go framework** and **`semvocab` library** while interacting with vehicles and C2 strictly over standard **OGC CS API**. | Preserves clean boundaries between **Part 1 (Specifications)**, **Part 2 (Bindings)**, OGC CSAPI/SensorML system interaction, human authority & custody lifecycles, and hierarchical capability composition. |

## How Research Maps to the AutonomyML Architecture

AutonomyML is organized across three architectural layers (see [AutonomyML Overview](../../AutonomyML%20Overview.md)):

1. **Layer 1 — Core Composition Language:** Capabilities, typed interfaces, process/behavior composition, FSM/BT primitive states and events, lifecycle, timing, and resource coordination.
2. **Layer 2 — Execution and Domain Profiles:** Supported SensorML methods, OGC API - Connected Systems (CSAPI) mappings, FSM/BT dialects, platform capabilities (e.g., aerial, ground rover, maritime), and domain-specific vocabularies.
3. **Layer 3 — Research Frontier Extensions:** Declarative planning, rich belief models, online learning, dynamic behavior generation, multi-agent coordination, and assurance/verification artifacts.
