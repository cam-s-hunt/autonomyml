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
