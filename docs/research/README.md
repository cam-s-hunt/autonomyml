# AutonomyML Architecture Research

This directory collects architectural research, comparative standards analyses, and schema prototypes supporting the design of the **Autonomy Model Language (AutonomyML)** specification.

## Research Documents

| Document | Focus | Relevance to [AutonomyML Overview](../../AutonomyML%20Overview.md) |
| :--- | :--- | :--- |
| [ASL & Complementary Open Standards Precedents](./asl-and-open-standards-precedents.md) | Architectural analysis of **Amazon States Language (ASL)** paired with **CNCF Serverless Workflow**, **W3C SCXML**, **BehaviorTree.CPP v4 / ROS 2 Nav2**, and **CEL (Common Expression Language)**, including OGC-native `camelCase` capability examples and unified FSM + Behavior Tree + SensorML/CSAPI blueprints for **Ground Rover** and **Aerial UxS (`Takeoff`, `Survey`, `ExecuteRTL`)** profiles (with standalone JSON files in [`examples/`](../../examples/)). | Maps external open standards directly to **Part 1 (Specifications)**, **Part 2 (Bindings)**, and all five concerns of the AutonomyML Implementation table (OGC CSAPI, SensorML, FSMs, BTs, and Executable Algorithms). |

## How Research Maps to the AutonomyML Architecture

AutonomyML is organized across three architectural layers (see [AutonomyML Overview](../../AutonomyML%20Overview.md)):

1. **Layer 1 — Core Composition Language:** Capabilities, typed interfaces, process/behavior composition, FSM/BT primitive states and events, lifecycle, timing, and resource coordination.
2. **Layer 2 — Execution and Domain Profiles:** Supported SensorML methods, OGC API - Connected Systems (CSAPI) mappings, FSM/BT dialects, platform capabilities (e.g., aerial, ground rover, maritime), and domain-specific vocabularies.
3. **Layer 3 — Research Frontier Extensions:** Declarative planning, rich belief models, online learning, dynamic behavior generation, multi-agent coordination, and assurance/verification artifacts.
