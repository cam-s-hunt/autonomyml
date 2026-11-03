# AutonomyML Architecture Research

This directory collects architectural research, comparative standards analyses, and schema prototypes supporting the design of the **Autonomy Model Language (AutonomyML)** specification.

## Research Documents

| Document | Focus | Relevance to [AutonomyML Overview](../../AutonomyML%20Overview.md) |
| :--- | :--- | :--- |
| [Reference Runtime & Standards Boundaries](./reference-runtime-module-boundaries.md) | Architectural separation between the **AutonomyML Mission Executive (`autonomyml-app`)**, **OGC CS API Servers (`semconnect`, OpenSensorHub)**, **OGC SensorML 3.0** (overlap vs. why AutonomyML is not a SensorML extension), and **existing brownfield automation stacks** (Part 2 bindings and thin edge protocol bridges without cross-system orchestration middleware). | Preserves clean boundaries between **Part 1 (Specifications)**, **Part 2 (Bindings)**, OGC CSAPI/SensorML system & process modeling, brownfield integration, human authority & custody lifecycles, and hierarchical capability composition. |

## How Research Maps to the AutonomyML Architecture

AutonomyML is organized across three architectural layers (see [AutonomyML Overview](../../AutonomyML%20Overview.md)):

1. **Layer 1 — Core Composition Language:** Capabilities, typed interfaces, process/behavior composition, FSM/BT primitive states and events, lifecycle, timing, and resource coordination.
2. **Layer 2 — Execution and Domain Profiles:** Supported SensorML methods, OGC API - Connected Systems (CSAPI) mappings, FSM/BT dialects, platform capabilities (e.g., aerial, ground rover, maritime), and domain-specific vocabularies.
3. **Layer 3 — Research Frontier Extensions:** Declarative planning, rich belief models, online learning, dynamic behavior generation, multi-agent coordination, and assurance/verification artifacts.
