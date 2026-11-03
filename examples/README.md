# AutonomyML Examples (`v0.1.0` Draft)

Standalone, machine-readable JSON examples of **AutonomyML Part 1 (`CapabilitySpecification`)** and **Part 2 (`CapabilityBinding`)** files so validators, visualizers, and execution runtimes can load them directly without parsing Markdown documents.

For the architectural rationale behind these examples, see [ASL & Complementary Open Standards Precedents](../docs/research/asl-and-open-standards-precedents.md).

## Naming Convention

* `*.spec.json` — **Part 1 (`CapabilitySpecification`):** Portable, platform-independent capability definition with OGC SensorML 3.0 / SWE Common 3.0 typed ports, CEL conditions/postconditions, and FSM + Behavior Tree control flow.
* `*.<system-id>.binding.json` — **Part 2 (`CapabilityBinding`):** Concrete system binding mapping symbolic capability resources to OGC API - Connected Systems (CSAPI) `/controlstreams`, `/datastreams`, `onHaltAction` preemption payloads, and SensorML computational processes.

## Example Catalog

| Domain Profile | Capability | Part 1 Specification | Part 2 Binding | Key Architectural Patterns |
| :--- | :--- | :--- | :--- | :--- |
| **Ground Rover** (`uxs-ground-rover:1.0`) | `WaypointNavigation` | [waypoint-navigation.spec.json](./ground-rover/waypoint-navigation.spec.json) | [waypoint-navigation.ugv-alpha-01.binding.json](./ground-rover/waypoint-navigation.ugv-alpha-01.binding.json) | Simple flat FSM (`states`), 2D `EPSG:4326` SWE Common ports, CEL sustained physical arrival `postcondition`, and verified zero-velocity `SafeHoldFallback`. |
| **Ground Rover** (`uxs-ground-rover:1.0`) | `GuardedWaypointNavigation` | [guarded-waypoint-navigation.spec.json](./ground-rover/guarded-waypoint-navigation.spec.json) | [guarded-waypoint-navigation.ugv-alpha-01.binding.json](./ground-rover/guarded-waypoint-navigation.ugv-alpha-01.binding.json) | Flat outer FSM hosting a `10 Hz` `behaviorTree` (`reactiveSequence` + `fallback` + `sensorMLProcess` local obstacle detour) over a SensorML-typed `blackboard`. |
| **Aerial UxS** (`uxs-aerial:1.0`) | `TakeoffSurveyAndRTL` | [takeoff-survey-and-rtl.spec.json](./aerial-uxs/takeoff-survey-and-rtl.spec.json) | [takeoff-survey-and-rtl.uav-quad-04.binding.json](./aerial-uxs/takeoff-survey-and-rtl.uav-quad-04.binding.json) | 3D `EPSG:4979` + explicit `AGL` clearances, nested SCXML-style parent modes (`AirborneEnvelope` $\supset$ `MissionFlight`) with `modeInvariants` and fault bubbling across `Takeoff` $\rightarrow$ `Survey` $\rightarrow$ `ExecuteRTL` / `EmergencyLandImmediate`. |
