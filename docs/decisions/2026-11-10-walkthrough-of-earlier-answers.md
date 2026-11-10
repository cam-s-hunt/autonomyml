# Walkthrough of the owner's earlier answers (2026-11-10)

Source: `_bmad-output/decisions-so-far.md` (written 2026-11-09). Each earlier answer was put to the owner one at a time in a card during a session with the ModSpec Architect on 2026-11-10. The outcome below is the owner's choice in that card, in the owner's words where they gave their own. Nothing here was sent to anyone, no gate config exists yet (`ogcspec.gate.toml` is absent), and no record was drafted.

Outcome key: **confirmed** (owner kept the earlier answer), **provisional** (kept until named research returns), **open** (not decided), **proposed** (a pattern recorded, not accepted).

## About the standard

| # | Earlier answer | Outcome |
|---|---|---|
| 1.1 | OGC Standard, developed in an SWG, written to the full ModSpec rules | confirmed (ModSpec edition and SWG still open) |
| 1.2 | One document with two parts (specifications, bindings) | confirmed |
| 1.3 | Requirements use "shall" as a starting point; any may later be downgraded | confirmed; the verbal form of each provision stays the owner's decision |
| 1.4 | Licence of text and examples is open; all rights reserved, brief attributed quotes, no republishing | open, working rule kept. The examples' author is not recorded. Note: the repository's `LICENSE` (MIT, Start Bootstrap LLC) appears to be the website template's licence and does not settle this |

## What it builds on

| # | Earlier answer | Outcome |
|---|---|---|
| 2.1 | Normative references: Connected Systems Parts 1 and 2 (23-001, 23-002), SensorML 3.0 (23-000), SWE Common 3.0, W3C SCXML, W3C PROV-O (six documents) | confirmed as a list. Editions are not pinned and the SWE Common number is not looked up. Adding them to the gate config is the owner's decision and was not done |
| 2.2 | Informative only: P-PLAN, BehaviorTree.CPP and ROS 2 Nav2 documentation | provisional: informative for now, **revisit after the behavior-tree research**. (The owner's free-text reply said "normative"; asked to clarify, the owner chose "informative for now, revisit after the research".) |
| 2.3 | SCXML for FSM execution semantics; own behavior-tree dialect; PROV-O for provenance; other candidates stay candidates | confirmed; the behavior-tree part to be revisited after the research |
| 2.4 | SOSA/SSN 2017 Recommendation | confirmed |

## Meaning and ontology

| # | Earlier answer | Outcome |
|---|---|---|
| 3.1 | Software and virtual systems count as systems; NCOR SOSA/SSN-to-BFO mapping can't be used as is; gap recorded, not resolved | confirmed |
| 3.2 | Author decides ontology mappings, with SWG review; links informative, terms clause normative | confirmed |
| 3.3 | A capability is a behaviour defined by a specification | confirmed as the definition. **Mapping proposed, not accepted:** capability (the specified behaviour) maps to CCO specification-type classes (Plan, `prescribes`); a system's ability to run it maps to CCO Agent Capability, borne by the executing host and linked by `concretizes`. The owner wants to map to CCO Agent Capability. Caveats: CCO's Agent is a material entity, so software itself is not the bearer; `prescribes` relates instances, which clashes with a specification that has no executor. See `_bmad-output/research-cco-capabilities.md` |
| 3.4 | Specification and binding are documents; encodings are other ways of writing the same document | confirmed |
| 3.5 | An executor is defined by what it does, not where it runs | confirmed |
| 3.6 | A state is defined by the six state types in the examples; SCXML's notion not adopted | **changed (direction chosen, wording not drafted):** on 2026-11-10 the owner chose "restate a minimal definition of your own": a state is a control mode of an automaton, distinct from system state (the world's condition) and from node status (a behavior-tree return value); the six example types become kinds of state under it. Exact wording is the owner's decision. The labelled-transition-system literature (Henzinger) is suggested by the report as an informative reference, not yet adopted. `csapiCommandAction` and `behaviorTree` match no standard state type (Architect's reading, not in the report). Research: `_bmad-output/research-state-and-control-models.md` |
| 3.7 | A postcondition is a condition over observations | confirmed |
| 3.8 | A terminal state is only succeed or fail; a third ending is open | **open, blocked on halt behaviour:** research is in (`_bmad-output/research-terminal-states.md`). On 2026-11-10 the owner chose to decide this together with the halt-behaviour design question, so two endings (succeed, fail) stand until then |

## Structure and scope

| # | Earlier answer | Outcome |
|---|---|---|
| 4.1 | Tests documents, and executors in a class of their own (nearly empty) | confirmed |
| 4.2 | Shared core targets any conformance target, no requirements yet; documents class for version and kind; specification, binding and encodings depend on both | confirmed |
| 4.3 | A binding must reference a specification that conforms to the specification requirements class, written as a requirement | confirmed, **with the ModSpec Part 1 clause 6.1.5 reading still to be checked against the clause text** |
| 4.4 | Provenance: one minimal executor requirement using a PROV-O Activity with the specification as Plan; contents and carrier open | confirmed |
| 4.5 | Transitions: four document-level rules from the examples; SCXML run-time semantics to the executor class | **confirmed** as the starting set after the research (2026-11-10). They apply to state machines only (behavior trees have no transitions). The "terminal state" rule is to be worded so it holds with two or three endings (see 3.8) |
| 4.6 | Behavior trees: document-level shape only; no node semantics | confirmed |
| 4.7 | Abstract requirements; separate JSON encoding split by document kind; JSON Schema not yet written | confirmed |
| 4.8 | Capability identifier form and authority left open | open (kept open) |
| 4.9 | Five of six suggested extra requirements kept; postcondition time limit dropped | confirmed. The earlier file names only four of the five kept; the fifth is **unidentified and must be named by the owner when drafting** |

## Corrections of fact

| # | Statement | Status |
|---|---|---|
| 5.1 | Connected Systems carries a per-term ontology address in the source citation of each SOSA/SSN-derived term | **partly confirmed** (agent check, 2026-11-10): true in the AsciiDoc source (10 terms in Part 1, 11 in Part 2); the published HTML (Approved 1.0, 2025-07-16) drops the IRI and renders an empty locality. Why it is dropped is the agent's inference, not verified. Report: `_bmad-output/research-cs-api-fact-check.md` |
| 5.2 | Resources are named symbolically inline (`resource`, `observationStream`, `sourceStream`), not declared in a block | verified against `examples/` on 2026-11-10 (the "in the blackboard" detail was not checked) |
| 5.3 | Command-issuing constructs are both states and behavior-tree nodes | verified against `examples/`: `csapiCommandAction` states, and tree nodes carrying a `resource` and `observationStream` |
| 5.4 | Parts 1 and 2 cite bibliography keys that do not exist (`SOSA/SSN`, `ISO19101`, `ISO19143`) | **mostly confirmed** (same report): `ISO19101` and `ISO19143` are cited in both Parts with no entry in either; `SOSA/SSN` has an entry under the key `SOSA-SSN`, so the slash form is an unresolved cross-reference in three term entries. Extra finding: Part 2 has a malformed `[[[OMS: ISO 19156:2011]]]` reference missing from the rendered list. The draft question to the maintainers was not sent; sending it is the owner's decision |

## Still open

All items in the earlier file's final section stay open: definitions of the standard's own words, pinned editions, execution-record contents, behavior-tree dialect and halt behaviour, version format, resource-name syntax, how a binding's reference is resolved, publication and discoverability, the media type, the owner's four design questions (CEL functions, explicit halt action, mode invariants and entry/exit hooks, compact JSON shorthand), and any ontology mapping. Notes from today:

- Behavior-tree dialect: no behavior-tree standard from W3C, IEEE, ISO, OGC or OMG was found; the only standards-track attempt found is ROS REP-2018 (status "Proposed", informational, absent from the official REP index). See `_bmad-output/research-behavior-tree-standards.md`.
- The owner asked for research into `ontology.nass.ai`. That hostname does not resolve; the agent reviewed `ontology.naas.ai` (NaasAI, Inc.) on the assumption of a typo, **confirmed by the owner later on 2026-11-10: `ontology.naas.ai` is the intended site**. It did not solve the software-agent problem and is not citable as a normative reference. See `_bmad-output/research-ontology-nass-ai.md`.

## Research reports produced on 2026-11-10 (agent-written, not yet reviewed by the owner)

- `_bmad-output/research-behavior-tree-standards.md`
- `_bmad-output/research-ontology-nass-ai.md`
- `_bmad-output/research-cco-capabilities.md`
- `_bmad-output/research-state-and-control-models.md`
- `_bmad-output/research-terminal-states.md`
- `_bmad-output/research-cs-api-fact-check.md`

## Other changes made in the session

- Created `AGENTS.md` and `CLAUDE.md` at the repository root, each with the note that questions and decisions for the owner are asked one at a time in a card, with plain-English context.
- Committed on 2026-11-10 at the owner's request (everything except the git-ignored `_bmad-output/`, so the reports and `decisions-so-far.md` it references are not in the commit).

## Follow-ups from the owner, later on 2026-11-10

- **naas.ai:** the owner confirmed `ontology.naas.ai` is the right site. The research already run on it (`_bmad-output/research-ontology-nass-ai.md`) found it does not let a software agent bear Agent Capability without a material bearer and is not citable as a normative reference; the agent read it through a summarising fetch tool, not raw HTML.
- **Fifth extra requirement (4.9):** searched the tracked repository, `_bmad-output/` and the session memory folder. The only record is the one sentence in `_bmad-output/decisions-so-far.md`, which names four. The fifth is **not recorded anywhere found** and is still unidentified. Nothing was guessed.
- **ModSpec clause 6.1.5 (4.3):** the owner asked for the reading to be checked against the clause text. Check in progress; result will be in `_bmad-output/research-modspec-clause-6-1-5.md`. The reading itself remains the owner's decision.
- **Licence (1.4):** stays open (owner, 2026-11-10).
- **Capability identifier (4.8):** stays open (owner, 2026-11-10). The owner asked for a deep recon on formal definitions of capability in the context of what the standard models, with possible inspiration from the US Department of War's Mission Engineering constructs and associated ontologies. In progress: `_bmad-output/research-capability-definitions-and-identifiers.md`.
- **Gate config:** to be written "when we think we're ready" (owner). Not written. `ogcspec.gate.toml` does not exist yet.
