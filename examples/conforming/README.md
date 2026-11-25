# Conforming example (proposal, not validated)

`waypoint-navigation.spec.json` and `waypoint-navigation.ugv-alpha-01.binding.json` re-express the simple ground-rover example (`../ground-rover/waypoint-navigation.*`) in the shapes decided so far (all `status: proposed` records under `records/`). The earlier examples in the other folders are untouched and do **not** conform.

**Not checked:** the documents were checked only by a hand-written structural script (members present, names unique, targets exist, binding keys match the specification). The CEL conditions were not type-checked, the SWE Common components were not validated against the pinned schemas, and the identifiers (`example.org` URIs) are placeholders; none is an assigned identifier.

## What the exercise showed (gaps, not decisions)

1. **No run-time inputs.** A run command carries only references, and command parameters are constants. The target waypoint (50.0, 8.0) is therefore fixed in the document. The earlier example took it as an input port, which the decided shapes cannot carry.
2. **No distance function.** "Arrived" is a postcondition comparing latitude and longitude within a fixed tolerance, written with four comparisons. CEL has no absolute-value function without an extension, and the standard's own function set is deferred.
3. **No sustained postcondition.** Postconditions are checked once, so the earlier "within the radius for 2 seconds" cannot be expressed.
4. **Redundant hold command.** The exit action `BrakeOnExit` and the state `SafeHold` both send the hold command, because a transition performs the exit actions of the state it leaves. Authors may need to avoid sending the same command twice.
5. **Stale readings in `SafeHold`.** The velocity data stream is read from entry; if it is stale there, the condition is not met and the timeout (30 s) ends the run in `SafeHoldTerminated`.
6. **Error names are lost.** The earlier example named errors (`AutonomyML.SafeStateEngaged`) and a `cause` text; the decided cause is only the name of a state, action or postcondition.
7. **Arrival depends on both the command status and the postcondition.** The transition is taken on status `COMPLETED`; the postcondition is checked only afterwards, at the succeed terminal state, so a command that completes away from the target ends the run as fail.


## Guarded example (`guarded-waypoint-navigation.*`, proposal, not validated)

Re-expresses `../ground-rover/guarded-waypoint-navigation.*`. Same checks as above (hand-written structural script only; CEL not type-checked; SWE Common not validated; `example.org` identifiers are placeholders). It uses a mode (`ActiveNavigation`) holding the command state, two mode-level invariants, mode-level transitions, a mode timeout and a mode exit action.

### What the exercise showed (gaps, not decisions)

1. **No behavior tree and no SensorML process.** The 10 Hz reactive sequence, the fallback and the `ComputeLocalDetour` process do not carry over: the detour planner, its blackboard and `processBindings` are dropped. The example drives straight to the target and holds if anything goes wrong.
2. **Geofence is a constant box.** The earlier example took a polygon as a run-time input and used `withinPolygon`. The decided shapes carry no run-time inputs and no geometry function, so the fence is a latitude and longitude box written with four comparisons.
3. **Battery reserve is a constant** (`20.0`), no longer a parameter.
4. **No sustained postcondition** (as in the first example): the 2 s and 1 s sustain times are lost.
5. **Invariants break at start if the data is stale.** The invariants are checked on entering `ActiveNavigation`; a run that starts before the first fresh pose or battery reading counts as broken and goes to `SafeHold` at once.
6. **Mode-level transitions and exit action.** `BrakeOnExit` is on the mode, so it also runs on the way to `Arrived`. Both mode transitions fire while the child is current (decided 2026-11-13); the mode timeout runs from entry to the mode. `SafeHold` and `BrakeOnExit` again send the same hold command twice (gap 4 above).
7. **Cross-mode targets.** The mode's invariants, transitions and timeout name states outside the mode. The records allow this ("a state of the same state machine"), but no requirement says so for a mode, and no test covers it.
8. **Error names are lost** (as above): `GeofenceBreach` and `LowBatteryReserve` survive only as the invariant names, which become the cause.
9. **A mode with a single child** is legal but adds nothing here except a place for the mode-level members; it shows the rules, not a real need.

## Aerial example (`takeoff-survey-and-rtl.*`, proposal, not validated)

Re-expresses `../aerial-uxs/takeoff-survey-and-rtl.*`. Same checks as above (structural script only; CEL not type-checked; SWE Common, including the `DataArray` of waypoints, not validated; `example.org` identifiers are placeholders). Three levels of nesting: `AirborneEnvelope` holds `MissionFlight` (holding `Takeoff` and `Survey`), `ReturnHome` and `AbortReturnHome`; `EmergencyLandImmediate` and the two terminal states are at the top level.

### What the exercise showed (gaps, not decisions)

1. **No choice state, so the return state is written twice.** The original ran one `ExecuteRTL` and then chose succeed or fail from `lastFault`. There is no choice kind and no shared blackboard, so the example has `ReturnHome` (ends succeed) and `AbortReturnHome` (ends fail), identical except for their transitions.
2. **No terminal state inside a mode.** The original ended `succeed` inside `AirborneEnvelope`. The records leave a terminal inside a mode open, so all terminal states are at the top level.
3. **A condition that mixes streams is not met until every stream has a value.** "Not met" applies to the whole condition, so `takeoff FAILED || trajectory FAILED` would never fire while the trajectory stream has no command. Each stream's failure is therefore its own transition. Authors must know this; no requirement says it in these words.
4. **Entry-action failures end the run as fail.** A failed `StartCapture` command goes to the run's `fail` ending by `action-failure`, not to a return home (the original sent `CSAPI.CommandFailed` to `ExecuteRTL`). A fallback after an action failure cannot be written.
5. **Everything the earlier example computed or took as input is a constant.** The coverage path generator (a SensorML process), the survey polygon, the airspace volume, the home position and the altitudes are constants: the transect is three fixed waypoints, the airspace is a box plus a ceiling, there is no `capturedImageCount` output, no `lastFault` and no sustained postcondition.
6. **Guards cover the whole `MissionFlight`.** The original checked geofence, wind and battery reserve only during `Survey`; they now also apply during `Takeoff`, and a data stream with no fresh value breaks them at entry (as in the guarded example).
7. **Boolean fields need no declaration.** `armed` and `transectCaptureComplete` are read without a `fields` entry because only quantities and arrays are declared; the `payload` stream therefore has no `fields` member. Scalar results (`wind`, `battery`) omit `path`.
8. **Camera and RTL home are placeholders.** The camera command shape (`trigger`) and the RTL command parameters are invented to have something to send; the earlier `onHaltAction` loiter and camera-stop payloads are dropped, and a camera stop is an exit action of `Survey`.
9. **Which command is "latest" on a shared stream** (open in the decision record) matters here: `rtl` is read in both return states, and `trajectory` may hold an old command from an earlier run.
