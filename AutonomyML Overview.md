# Autonomy Model Language

## A robust and semantically-grounded means of defining autonomous capabilities

# WHY?

- Enhance interoperability of autonomous systems  
- Describe equivalent behaviors between autonomous frameworks  
- Iterative development across the spectrum of autonomy

# Overview

AutonomyML defines reusable autonomous capabilities and composes their data processing, state transitions, and behavioral execution.

## Part 1 \- Specifications

\- Typed Interfaces  
\- Execution Lifecycles  
\- State/Event Exchange  
\- Resource Coordination

Part 2 \- Bindings  
\- Computational Methods   
\- System Interactions  
\- Concrete Implementations.

# Goal

AutonomyML ensures that different independent autonomous UxS system implementations publish their autonomy capabilities openly via a standard that enables the description of equivalent observable behavior, without relying on undocumented conventions inside its components.

# Implementation

AutonomyML relies on the OGC API \- Connected Systems Standard (CSAPI) and SensorML standards as well as formalisms from Finite State Machines (FSM) and Behavioral Trees (BT) to create executable models of autonomous capabilities:

| Concern | Mechanism | What it provides |
| :---- | :---- | :---- |
| Interaction with a particular system | OGC CSAPI | System-facing observations, commands, and command-status resources.  |
| Computational functions and dataflow | SensorML | Typed inputs, outputs, parameters, methods, and hierarchical process composition. Its framework includes computational processes, sensors, and actuators—not just sensor metadata. |
| Modes and transitions | FSMs | Explicit state-oriented behavior management.  |
| Reactive task composition | BTs | Hierarchical selection and sequencing of conditions and actions, with execution status propagated through the tree.  |
| Executable algorithms | Process implementations and system implementations | The actual perception, estimation, planning, control, or other computations invoked through these models. SensorML describes their interfaces and methodology; an execution environment supplies support for those methods. |

# AutonomyML Architecture

| Layer | Scope |
| :---- | :---- |
| Core composition language | Capabilities, typed interfaces, process/behavior composition, FSM/BT primitive states & events, lifecycle, timing, and resource coordination. |
| Execution and domain profiles | Supported SensorML methods, OGC CSAPI mappings, FSM/BT dialects, platform capabilities, and domain-specific meanings. |
| Research frontier extensions | Declarative planning, rich belief models, online learning, dynamic behavior generation, multi-agent coordination, and assurance artifacts. |

