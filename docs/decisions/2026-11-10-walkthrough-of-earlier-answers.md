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
| 3.8 | A terminal state is only succeed or fail; a third ending is open | **open, blocked on halt behaviour:** research is in (`_bmad-output/research-terminal-states.md`). On 2026-11-10 the owner chose to decide this together with the halt-behaviour design question, **superseded by the decision below (2026-11-10, later): a third ending is chosen in principle** |

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

## Gate-config prerequisites decided by the owner, 2026-11-10 (later)

- **ModSpec edition (1.1):** "use the latest ModSpec edition available". The latest the lookup found is OGC 08-131r7 (ModSpec Part 1: Core, v1.1, approved 2026-03-05, published 2026-05-21), which is also the edition the gate cites. Whether a newer edition exists was not independently checked beyond that lookup.
- **`core_dependency`:** `direct` (the literal reading of Requirement 22). This settles the contested Req 22 reading for the gate; it does not change answer 4.3.
- **`namespace`:** left empty for now. The owner expects to propose their own autonomy domain ontology (extending BFO, CCO and SOSA/SSN, and including the concepts of https://ceur-ws.org/Vol-3050/Paper1.pdf plus other autonomy ontologies found) and to ground the namespace in it. That is an expectation, not a decision; a recon is running (`_bmad-output/research-autonomy-ontologies.md`).
- **Clause 6.1.5 check:** result in `_bmad-output/research-modspec-clause-6-1-5.md`. The clause is a definition with an example close to answer 4.3; the standard's own note under definition 6.3.11 says "the testing of indirect dependencies seems to violate this definition". The reading stays the owner's.
- **Gate config:** written on 2026-11-10 with the owner's yes: `ogcspec.gate.toml` at the repository root with three lines (`records_dir = "records"`, `core = "/req/core"` as a proposed identifier, `core_dependency = "direct"`). No namespace, pins, ontologies, style rules or baseline yet. The gate has not been run (no records exist).

## Ontologies called out explicitly, 2026-11-10 (later)

- **Decision (owner):** the standard explicitly names **SOSA/SSN, BFO and CCO** as ontologies it uses and references, and treats **all three as normative references** (chosen over "BFO and SOSA/SSN normative, CCO informative", which the Architect had recommended because CCO's web addresses point at a moving development branch, CCO 3.0 is due 2026-12-31 and will restructure its information classes, and CCO's Agent is defined as a material entity).
- **Adds to answer 2.1:** the normative list grows from six documents to nine (the earlier six plus SOSA/SSN, BFO and CCO). Answer 2.4 already fixes SOSA/SSN as the 2017 W3C Recommendation.
- **Still open, owner's to decide:** the exact editions to pin. Candidates from the research: BFO as ISO/IEC 21838-2 (edition not yet recorded), CCO as the v2.2 release tag (the research advised citing the release tag and its SHA-256 rather than the IRI). Not verified by the Architect beyond the research reports.
- **Interaction with answer 3.2:** that answer says ontology links in the text are informative by default and the terms-and-definitions clause is normative. Making the ontologies normative references does not by itself make any term mapping normative; mappings stay proposals, informative by default, until the owner says otherwise.
- **Known risk accepted by this choice:** a normative reference to CCO ties conformance to one CCO release; CCO 3.0 may force a revision. The tension between CCO's material-entity Agent and software counting as a system (answer 3.1) is unresolved.
- **Gate config:** not changed. Declaring the three in `[[ontologies]]` and `[[normative_references]]` needs the pins above and a separate yes.

## Ontology direction, 2026-11-10 (later)

Owner decisions after the autonomy-ontologies and capability-definitions recons:

1. **The standard will have its own ontology** (the owner's words: "We are going to write our own ontology"). This replaces the earlier "expectation"; it extends BFO, CCO and SOSA/SSN. Scope, name, IRIs, namespace and governance are not decided. Research: `_bmad-output/research-autonomy-ontologies.md`, `_bmad-output/research-capability-definitions-and-identifiers.md`.
2. **Mapping priority:** "It's more important to map to BFO/CCO than directly to SOSA."
3. **SOSA still used** for concepts the standard pulls from SensorML and the Connected Systems API: those terms are SOSA-mapped.
4. **Not decided and flagged by the research:** how software and virtual systems fit (CCO Agent is a material entity); whether "capability" remains the name of the specification document given that DoD, UAF, CCO and IOF all use "capability" for an ability; the identifier and namespace; and whether to pin CCO v2.2 given that the CCO Governance Board recommends users wait for CCO 4.0 (3.0 expected by 2026-12-31, 4.0 by 2027-06-30; per `research-autonomy-ontologies.md` section 2.7, not independently checked).

## Candidate edition pins, from research (not accepted by the owner)

Source: `_bmad-output/research-edition-pins.md` (research date 2026-11-10; agent-written, summary table read by the Architect, details not all re-checked). **Nothing below is pinned in any config; each pin is the owner's decision.**

| Document | Number | Edition / date found | Notes |
|---|---|---|---|
| OGC API - Connected Systems Part 1 | OGC 23-001 | v1.0, approved 2025-06-02, published 2025-07-16 | Corrects an earlier note: 2025-07-16 is the publication date, not approval |
| OGC API - Connected Systems Part 2 | OGC 23-002 | v1.0, same dates | |
| OGC SensorML | OGC 23-000 | v3.0, same dates | Official title "OGC SensorML Encoding Standard" |
| OGC SWE Common Data Model | **OGC 24-014** | v3.0 ("3.0.0" on the cover), same dates | Fills the earlier unknown document number |
| W3C SCXML | none | Recommendation 2015-09-01 | No newer version; 7 editorial errata |
| W3C PROV-O | none | Recommendation 2013-04-30 | No newer version; 6 non-normative errata |
| W3C SOSA/SSN | none | Recommendation 2017-10-19 | A "2023 Edition" Working Draft is active (latest 2026-11-04), not citable except as work in progress |
| BFO | ISO/IEC 21838-2:2021 | Edition 1, 2021-11-30 | Text availability unresolved (price unclear); free electronic inserts exist; the GitHub `bfo-core.owl` differs from the ISO insert |
| CCO | none | Release tag `v2.2`, 2026-08-14, tag commit `0bc7d33e1bc09fd4693366119ab4e03cb0340042`, BSD-3-Clause | CCO IRIs redirect to the moving `develop` branch; tag commit is not in `develop` history; CCO 3.0 planned by 2026-12-31 |

## SOSA/SSN pin, 2026-11-10 (later)

Owner chose to **pin the 2017 W3C Recommendation** (https://www.w3.org/TR/2017/REC-vocab-ssn-20171019/), consistent with answer 2.4 and with Connected Systems 1.0, and to **note that a "2023 Edition" Working Draft is in active development** (latest dated 2026-11-04). Revisit when that edition becomes a Recommendation. The other eight pins in the candidate table remain candidates, undecided. Nothing is written to `ogcspec.gate.toml`.

## Eleven decisions on the ontology and identifiers, 2026-11-10 (later)

Recorded as given by the owner. Working notes for the ontology are in `docs/ontology/autonomy-ontology-notes.md`.

1. **Terminology:** use **capability specification** and **capability binding** instead of bare "capability". Whether bare "capability" is defined at all, and the identifier's type segment, are not decided. (Related: answer 3.3 and the proposed mapping pattern there.)
2. **Authority, delegation and boundary terms** are to be captured in the ontology notes. Done as a first pass: notes section 2.
3. **State** must also be defined in the ontology. Done as a pointer: notes section 3 (answer 3.6 holds).
4. **SSN-to-BFO/CCO mapping as the default route**, if it resolves or eases mapping, instead of mapping from SOSA directly. **Conditional:** the research (`_bmad-output/research-ssn-bfo-cco-mapping.md`) is checking whether such a mapping exists and whether it covers non-material systems; the earlier note was that the NCOR mapping is material-only.
5. **SOSA `System` is a valid approach until the new CCO comes out.** Working approach. Whether SOSA `System` can be non-material was not verified at the time of the decision; the research above is checking.
6. **Behavior is treated as an information carrier** (information plus carrier option: the behavior is information, the executing system bears the ability).
7. **Pin current CCO** (release tag `v2.2`), adapt later. Pin details in the notes, section 9. The CCO Governance Board's advice to wait for 4.0 was noted. Not written to the gate config.
8. **Adopt OPTaC concepts, updated to the latest CCO terms.** Which terms exactly, and what to do about Play's competitive context, remain open (notes section 6).
9. **Mission specification patterns are inspiration** for states and behavior-tree primitives. The pattern list has not yet been read here (notes section 7).
10. **Do not import "those three"; cite them informatively.** The Architect read "those three" as SkiROS2, SOMA and OMG ROSO. **Confirmed by the owner (SkiROS2, SOMA, OMG ROSO).**
11. **Identifiers:** use `urn:autonomyml`, and **prepare instructions for the owner to register it**; keep to **OGC's register statuses** for identifier lifecycle. The instructions are being drafted at `docs/identifiers/urn-autonomyml-registration-guide.md`. **Nothing is registered or submitted; registration is the owner's action.** Until it is registered, `urn:autonomyml:...` is not a valid URN under RFC 8141 section 1 (`research-capability-definitions-and-identifiers.md`). The segments after `urn:autonomyml:` are not decided. The gate config's `namespace` (the document's URI namespace) stays empty, as it is a separate matter. This supersedes the "capability identifier form and authority left open" part of answer 4.8 for the scheme only; authority and segment structure remain open.

## Pins accepted, 2026-11-10 (later)

The owner accepted all seven remaining candidate pins. Together with the two decided earlier, the nine pinned normative references are:

| Document | Pin |
|---|---|
| OGC API - Connected Systems Part 1 (OGC 23-001) | v1.0, approved 2025-06-02, published 2025-07-16 |
| OGC API - Connected Systems Part 2 (OGC 23-002) | v1.0, same dates |
| OGC SensorML (OGC 23-000) | v3.0, same dates |
| OGC SWE Common Data Model (OGC 24-014) | v3.0, same dates |
| W3C SCXML | Recommendation, 2015-09-01 |
| W3C PROV-O | Recommendation, 2013-04-30 |
| W3C SOSA/SSN | 2017 Recommendation, 2017-10-19 (a 2023 Edition draft is in progress) |
| ISO/IEC 21838-2 (BFO) | Edition 1, 2021-11-30; the free BFO file on GitHub differs from the ISO insert and has changed since its 2024-01-29 release, so the standard cites the ISO edition and states which free file it mirrors |
| CCO | release tag `v2.2`, 2026-08-14, tag commit `0bc7d33e1bc09fd4693366119ab4e03cb0340042`; to be adapted later |

**Where these pins live:** in the standard's normative-references clause. They are **not** all gate-config entries: the gate's `[[normative_references]]` entries (name, `uri_prefix`) are only for *external requirements classes* that this standard's classes inherit, and `[[ontologies]]` (key, optional `iri_prefix`) are only for term mappings. (Correction of the Architect's earlier statement that the pins would go into the gate config.) `ogcspec.gate.toml` is unchanged.

## URN registration guide delivered, 2026-11-10 (later)

`docs/identifiers/urn-autonomyml-registration-guide.md` (agent-written from RFC 8141 and other primary sources; reviewed by the Architect, not by the owner). Nothing was submitted, registered or sent; all commitment fields are marked `OWNER TO DECIDE`. Findings: `autonomyml` passes the RFC 8141 NID syntax tests and was not in the IANA registry (last updated 2026-10-28; re-check before submitting). A trademark or name-confusion check was not done (a similar string "AutonoML" appears in search results). Submission goes to the discussion list `urn@ietf.org` (`urn-nid@` is discontinued per RFC 8141 section 7.3). The fast-track route requires a recognized standards body and the IESG decides recognition; whether this standard or OGC would qualify is not established. OGC Naming Authority procedures 09-046r6 define **eleven** status flags (deprecated, experimental, invalid, notAccepted, proposed, reserved, retired, stable, submitted, superseded, valid), and the text is inconsistent on whether a new item starts as `submitted` or `invalid`.

## Identifier lifecycle statuses, 2026-11-10 (later)

Owner chose **all eleven** OGC Naming Authority status flags (09-046r6 clause 7.3): `deprecated`, `experimental`, `invalid`, `notAccepted`, `proposed`, `reserved`, `retired`, `stable`, `submitted`, `superseded`, `valid`. Rules carried with it: a superseding item points to its predecessor; an assigned URN is never reassigned (RFC 8141 section 5). Not decided: the exact wording and the mapping of statuses to a URN namespace specification; the source's inconsistency on whether a new item starts as `submitted` or `invalid`, which would be put to the OGC Naming Authority by the owner if it matters. Nothing sent to OGC.

## Mission specification patterns read, 2026-11-10 (later)

Decision 9 follow-up done: the catalogue (22 patterns: 10 core movement, 6 avoidance, 6 triggers) was read via `_bmad-output/research-mission-patterns.md` and summarised in `docs/ontology/autonomy-ontology-notes.md` section 7, as options for states, behavior-tree primitives and observation-based postconditions. The patterns do not mention behavior trees, FSMs or SCXML. No primitive is adopted; the owner chooses.

## SSN mapping route decided, 2026-11-10 (later)

Research: `_bmad-output/research-ssn-bfo-cco-mapping.md` (agent-written; the Architect read the findings, the term and option tables and the software sections; no reasoner was run).

- **Decision 4 resolved:** the owner chose to **adopt the W3C SOSA/SSN 2023 Edition BFO/CCO alignment module (WD section 7.1.3) as the default** for mapping SOSA/SSN terms, over (a) reusing the agreed terms with own System axioms, which the Architect had recommended, and (b) mapping from SOSA in the standard's own namespace. NCOR's mapping is not adopted (it makes System material).
- **Reconciliation with the 2017 pin (owner chose):** the 2017 Recommendation stays the normative reference; the 2023 module is used as an **alignment source** and cited informatively as work in progress, with the module's 2023 terms translated to the 2017 ones (`sosa:System` to `ssn:System`) where they differ, and each correspondence recorded. Nothing normative depends on the draft.
- **Decision 5 holds with a caveat:** SOSA `System` imposes no materiality (both editions). Under the W3C module a System is an independent continuant, which allows non-material systems but not code-only ones; software is placed through the carrier-plus-role route (material computer bears a role or function that concretizes the code), which neither mapping provides and the ontology must add.
- **Known risks accepted:** the module is non-normative and may change before it becomes a Recommendation; it contains a Turtle typo that drops one axiom; it relies on an unversioned CCO import and a CCO 2.1+ term; IRIs differ between 2017 and 2023.

## Third ending chosen, 2026-11-10 (later)

Decision 3.8 / halt behaviour (part): asked whether a run stopped from outside (an operator, a supervising system or an authority) should be its own ending, separate from succeed and fail. The owner chose **yes, a third ending**. Recommendation followed; reasons given were that the Connected Systems API (COMPLETED, FAILED, CANCELED), ROS 2 actions and Temporal already separate them, and that "the behavior's own problem" stays apart from "an authority stopped it".

- **Decided:** terminal endings are succeed, fail and a stopped-from-outside ending. The four-transition rule for terminal states (4.5) is to be worded to hold with three endings.
- **Not decided (still open):** the ending's name; its definition and wording; whether a stopped run may be restarted; who may issue the halt; whether the halted behavior gets a last step to clean up; whether the halt is an explicit action in the document (the owner's design question); how it maps to the CS API's CANCELED and to ontology terms. Nothing normative is drafted.

## Explicit halt action chosen, 2026-11-10 (later)

Owner design question "explicit halt action": the owner chose **yes, the document format has an explicit halt action**, a named step an authority can issue to stop a running behavior, rather than leaving halting to the executor and platform. Recommendation followed; reasons given were that conformance tests can then say "issue a halt, expect the stopped ending", and that it fits the authority-to-halt notes and the Connected Systems cancel command.

- **Decided:** an explicit halt action exists in the specification vocabulary and leads to the stopped-from-outside ending.
- **Not decided (still open):** its name and wording; who may issue it; what effect it has on the running behavior (for example a last clean-up step, as in SCXML `onexit` or Nav2 `on_cancelled`, versus immediate stop); whether a halted run can resume or restart; how it maps to the CS API cancel command and to ontology terms; and its place in the document kinds (state machine, behavior tree). Nothing normative is drafted.

## Halt effect chosen, 2026-11-10 (later)

Asked whether a halted behavior gets a last chance to clean up. The owner chose **a defined clean-up step, then the stopped ending** (recommendation followed; reason given: abrupt stops can leave physical systems unsafe, and SCXML exit handlers and Nav2's cancel handler are precedents).

- **Decided:** a halt runs a defined clean-up before the run ends in the stopped-from-outside ending.
- **Not decided (still open):** what the clean-up may do; what happens if it fails or overruns (including which ending results); whether a second halt can interrupt it; how it appears in state machines versus behavior trees (BehaviorTree.CPP `halt()` resets to IDLE and records no status); who may issue the halt; the names and wording; restart or resume. Nothing normative is drafted.

## Failed clean-up ends in fail, 2026-11-10 (later)

Asked which ending a run gets if the clean-up after a halt fails or runs too long. The owner chose **the fail ending, with the halt recorded as the cause** (recommendation followed; reason given: the stopped ending then means "stopped from outside and left in a defined, cleaned-up condition", and a failed clean-up is a real fault).

- **Decided:** the stopped-from-outside ending is reached only through a clean-up that completes; a failed or overrunning clean-up ends in fail, and the halt is carried as the recorded cause.
- **Not decided (still open):** the time limit and how it is set; the form of the recorded cause (it ties to the open execution-record contents); whether a second halt can interrupt clean-up; who may issue the halt; names and wording; restart or resume. Nothing normative is drafted.

## Entry and exit actions chosen, 2026-11-10 (later)

Owner design question "mode invariants and entry/exit hooks" (first half): asked whether a state may declare entry and exit actions, as SCXML `onentry` and `onexit` do. The owner chose **yes, both entry and exit** (recommendation followed; reasons given: the halt clean-up needs a home, SCXML runs exit actions for all active states on cancellation, and tests can observe them).

- **Decided:** a state in a state-machine document may declare entry actions and exit actions. They apply to state machines only; behavior trees have no states of this kind.
- **Not decided (still open):** the order in which they run; what happens if one fails (the halt case already ends in fail, see above); whether the halt clean-up is the exit actions of the active states or a separate named clean-up; what an action may contain; names and wording. **Mode invariants (the second half of this question) not yet asked.** Nothing normative is drafted.

## Halt clean-up is the exit actions, 2026-11-10 (later)

Asked where the halt clean-up lives. The owner chose **the exit actions of the states active when the halt arrives** (recommendation followed; reasons given: no new construct, matches SCXML cancellation, each state cleans up what it set up).

- **Decided:** for state machines, a halt leaves every active state, running each one's exit actions, and then the run ends in the stopped-from-outside ending (or in fail if an exit action fails or overruns, see above). No separate named clean-up construct.
- **Not decided (still open):** whether a leave caused by a halt can be told apart from an ordinary leave inside an exit action; the order of exit actions across nested or parallel states; the clean-up rule for behavior trees, which have no states; names and wording. Mode invariants not yet asked. Nothing normative is drafted.

## Halt for behavior trees deferred, 2026-11-10 (later)

Asked what the standard requires when a halt reaches a running behavior tree. The owner chose **defer; state machines first** (recommendation followed; reason given: behavior trees get document-level shape only, no node semantics, and no behavior-tree standard was found to follow).

- **Decided:** nothing is written about halting behavior trees for now; the question stays open. Consistent with decision 4.6.
- **Not decided (still open):** whether a behavior tree can be halted at all, whether it can end in the stopped ending, and how it would clean up (node-level handler, document-level rule, or none). Revisit with the behavior-tree dialect decision.

## Mode invariants chosen, 2026-11-10 (later)

Owner design question "mode invariants and entry/exit hooks" (second half): asked whether a state may declare a mode invariant, a condition that must stay true while the state is active. The owner chose **yes, as a condition over observations**, the same form as postconditions (decision 3.7) (recommendation followed; reasons given: reuses a confirmed form, lets tests check limits during a state).

- **Decided:** a state in a state-machine document may declare an invariant expressed as a condition over observations.
- **Not decided (still open):** what happens when an invariant is broken (which ending or transition; asked next); when it is evaluated (continuously, on each observation, on each step); how it interacts with the observation model and the CEL-functions question; names and wording. Nothing normative is drafted.

## Broken invariant: the specification names the response, 2026-11-10 (later)

Asked what happens when a state's invariant is broken while the state is active. The Architect recommended a fixed rule (the run ends in fail, with the broken invariant recorded as the cause). The owner **chose a different option: each invariant declares its own response in the specification** (a transition to another state, or a fail).

- **Decided:** a broken invariant triggers a response that the specification declares for that invariant; the standard does not fix one behavior for all.
- **Not decided (still open):** the form of the response (the list of permitted responses; whether "fail" is one of them or the default when none is declared); whether a specification must declare a response for every invariant; what a conformance test may assume when none is declared; when an invariant is evaluated; names and wording. Consequence the Architect noted: tests cannot assume one behavior, so they will check that the declared response occurs. Nothing normative is drafted.

## Invariant must declare a response, 2026-11-10 (later)

Asked what happens if an invariant declares no response. The owner chose **require a response; no default** (recommendation followed; reason given: it matches "the specification decides" and tests never guess).

- **Decided:** every invariant must declare a response; a specification that omits one does not conform. This closes the owner design question "mode invariants and entry/exit hooks" in outline.
- **Not decided (still open):** the list of permitted responses; when an invariant is evaluated; names and wording. Two of the owner's four design questions are now answered in outline (explicit halt action; mode invariants and entry/exit hooks). **Remaining: CEL functions and the compact JSON shorthand.** Nothing normative is drafted.

## CEL chosen as the condition language, 2026-11-10 (later)

The decision record showed no earlier decision on the expression language (CEL is recommended in `docs/research/asl-and-open-standards-precedents.md`, and the owner's design question mentions "CEL functions"). Asked whether the standard requires CEL for conditions (postconditions, invariants, transition guards). The owner chose **yes, CEL** (recommendation followed; reasons given: deterministic, cannot loop or change state, type-checkable before a mission).

- **Decided:** conditions in the standard are written in CEL.
- **Not decided (still open):** the CEL edition to pin (a tenth normative reference; CEL is not an OGC or W3C standard; the pin is the owner's decision, to be named); which functions are available (the owner's design question); how observations are exposed to a condition; whether CEL's own type checking is required before a run; names and wording. Nothing normative is drafted.

## CEL functions: built-in only for now, 2026-11-10 (later)

Owner design question "CEL functions": asked whether the standard defines its own functions beyond CEL's built-ins. The owner chose **built-in CEL only; the standard's own function set is a planned later extension** (recommendation followed; reason given: choosing functions, units and coordinate reference systems is a large decision not yet explored).

- **Decided:** the first version's conditions use only CEL's standard functions. The standard records its own function set as a planned extension.
- **Not decided (still open):** which CEL edition is pinned; which extension functions (distance, age of observation, etc.), their semantics, units and coordinate reference systems; how observations are exposed to a condition. Three of the owner's four design questions are now answered in outline. **Remaining: the compact JSON shorthand.** Nothing normative is drafted.

## JSON shorthand: full form only, 2026-11-10 (later)

Owner design question "compact JSON shorthand": asked whether value types in a specification use SWE Common 3.0 JSON verbatim or may also use a compact shorthand (`"uom": "m"`). The owner chose **full form only** (recommendation followed; reasons given: existing SWE Common tools and validators accept it, one form to test; a shorthand can be added later without breaking anything).

- **Decided:** documents use the SensorML 3.0 / SWE Common 3.0 JSON in full; no compact shorthand in the first version.
- **Not decided (still open):** nothing further on this question. A shorthand remains a possible later extension.

## All four owner design questions answered in outline, 2026-11-10 (later)

Explicit halt action: yes. Mode invariants and entry/exit hooks: yes (see above). CEL functions: built-in only for now. Compact JSON shorthand: full form only. Notes the Architect flags for later wording decisions (from the source of these questions, `docs/research/asl-and-open-standards-precedents.md` section 7):

- That research asked the halt question as a **binding** contract (each continuous control-stream binding declaring an `onHaltAction`, Part 2), while the owner's decisions above place the halt action and its clean-up in the **specification** (state exit actions). Where a binding says how a halt reaches the system's control stream is not decided.
- That research also asked whether invariants are evaluated on every incoming observation or at a declared tick rate. This is **still open**.
- Research examples use a parent state type named `"mode"`; no name is adopted.

## CEL pin chosen: v0.26.0, 2026-11-10 (later)

Asked which CEL specification release to name. The Architect recommended `v0.25.3` (three months old; `v0.26.0` was a day old). The owner **chose a different option: `v0.26.0`**.

| Item | Value |
|---|---|
| Source | `github.com/google/cel-spec` (public; looked up via the GitHub API on 2026-11-10; the repository has no 1.0 release, only `v0.x` tags) |
| Pinned release | tag `v0.26.0`, published 2026-11-09 |
| Tag commit | `21ec6f4e52e8d694687ff9ed7408d3eccbb955d7` |
| Previous releases | `v0.25.3` (2026-08-13, `ba58ae5007845f3a1279b488cdeb79645ce958bb`), `v0.25.2` (2026-05-08) |

- **Decided:** the standard names CEL `v0.26.0` as its pinned edition, the **tenth normative reference** (the owner's named pin). It is not an OGC, W3C or ISO standard.
- **Risks noted (not accepted or rejected by the owner beyond the choice):** the release was one day old when chosen, so problems with it would not yet be visible; the Architect has not read what changed between `v0.25.3` and `v0.26.0`; the project is pre-1.0, so later releases may break conditions written against this one; the tag commit is itself a 2026-10-27 commit ("Add conformance tests for NaN and -0.0 comparisons"), about two weeks before the tag was published.
- **Not decided (still open):** the exact way the pin is worded in the normative-references clause; whether CEL's type checking is required before a run; the re-pin policy. Nothing normative is drafted.

## Invariant timing: each new observation, 2026-11-10 (later)

Asked when a state's invariant is checked while the state is active. The owner chose **each new observation** (recommendation followed; reasons given: no extra setting, cannot miss a change, testable).

- **Decided:** an invariant is checked whenever a new observation relevant to it arrives while the state is active.
- **Not decided (still open):** what "relevant" means (which observations trigger which invariant); whether it is also checked on entry to the state; a stale-data rule for an invariant on a silent sensor (not handled by this decision); how an executor that receives observations in batches or out of order behaves; names and wording. Nothing normative is drafted.

## Invariant checked on entry, 2026-11-10 (later)

Asked whether an invariant is also checked when its state is entered. The owner chose **yes, check on entry** (recommendation followed; reason given: closes the gap where a state starts in an unsafe condition and is not noticed until the next observation).

- **Decided:** on entering a state, its invariants are checked against the latest observations before the state does anything else; a broken invariant triggers its declared response at once.
- **Not decided (still open):** the order relative to the state's entry actions (the wording above says "before the state does anything else", which would put the check before entry actions; not confirmed as the owner's intent); what the "latest observation" is when none has arrived yet (is the invariant true, false or unknown?); whether a response triggered on entry still runs the state's exit actions; names and wording. Nothing normative is drafted.

## Invariant with no data counts as broken, 2026-11-10 (later)

Asked how an invariant counts on state entry when no observation has arrived yet for something it reads. The owner chose **broken until data arrives** (recommendation followed; reason given: "no evidence" should not pass as "safe" for safety limits).

- **Decided:** an invariant whose inputs have no observation yet is treated as broken, so its declared response happens.
- **Not decided (still open):** what counts as "no observation" for an input that has reported before but has gone silent (a stale-data rule: not decided here); how a specification can enter a state that depends on a slow-starting sensor (for example by declaring a response that tolerates it, or by entering the state only after the sensor reports); whether CEL's handling of missing values needs a rule; names and wording. This, together with the timing and entry decisions above, completes the invariant evaluation rules in outline. Nothing normative is drafted.

## Draft wording for "state" chosen, 2026-11-10 (later)

Asked which of two drafts to take forward as the proposed wording for the definition of **state** (decision 3.6, direction: control mode of an automaton). The owner chose **draft A, definition plus two notes** (recommendation followed). This is the chosen **draft**; it has **not been marked accepted as final wording** (see "How to read this" below).

> **state**: control mode of an automaton, declared by a capability specification, in which an executor performs the behavior that the kind of the state prescribes.
>
> NOTE 1  A state is not the condition of a system or of its environment (system state), and is not the status returned by a behavior-tree node.
>
> NOTE 2  The kinds of state are defined in the requirements class for capability specifications. *(Kinds not yet decided.)*

- **Not decided (still open):** which kinds of state exist (the six example types, plus whatever the halt and invariant decisions add); how many states can be active at once (nested or parallel states); whether "executor" and "capability specification" are defined first, since this definition depends on both; final acceptance of the wording; its mapping to the ontology (control mode of an automaton; the ontology notes section 3 says wording is the owner's).
- **How to read this:** the Architect proposes wording and the owner picks; a definition counts as accepted only when the owner says so in these terms. Terms this draft depends on: capability specification, executor, automaton (not yet defined).

## "state" wording accepted for now, 2026-11-10 (later)

Asked whether draft A is accepted as the final wording. The owner chose **accept for now** (recommendation followed): the wording above is **accepted**, **subject to** the terms it depends on (capability specification, executor, automaton) being defined; if any of them changes, the definition comes back to the owner. It is recorded here only; no normative file contains it.

- **Still open for this term:** the kinds of state; how many states are active at once; the ontology mapping.

## Draft wording for "capability specification" chosen, 2026-11-10 (later)

Asked which draft to take forward for **capability specification** (decisions 3.3 and 3.4: a specification is a document; a capability is a behavior defined by a specification). The owner chose **draft A** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **capability specification**: document that defines a behavior as a state machine or a behavior tree.
>
> NOTE 1  The behavior defined by a capability specification is the capability. *(Depends on whether bare "capability" is defined; undecided.)*
>
> NOTE 2  A capability specification is not tied to a particular system; a capability binding ties it to one.

- **Not decided (still open):** what the document must contain (interface, postconditions, other content: left to the requirements, and reported as a gap); whether bare "capability" is defined; the definition of "capability binding" that Note 2 relies on; the "state machine" and "behavior tree" terms; final acceptance.

## "capability specification" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** for draft A of **capability specification** (recommendation followed). Accepted wording, recorded here only, **subject to** "capability binding", "state machine", "behavior tree" and bare "capability" being defined; it comes back to the owner if one of them changes. No normative file contains it.

## Draft wording for "executor" chosen, 2026-11-10 (later)

Asked which draft to take forward for **executor** (decision 3.5: defined by what it does, not where it runs). The owner chose **draft A** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **executor**: system that runs a capability specification, by entering and leaving its states or by evaluating its behavior tree.
>
> NOTE 1  The definition says nothing about where an executor runs.
>
> NOTE 2  Requirements on how an executor runs a capability specification are in the requirements class for executors.

- **Not decided (still open):** acceptance; the ontology mapping (software and virtual systems count as systems; behavior as information carried by the executing system); whether the "system" in the wording needs its own definition (SOSA/SSN `System` is the working approach); what an executor must do (state changes, halt, provenance: executor requirements class, nearly empty for now).

## "executor" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** for draft A of **executor** (recommendation followed). Accepted wording, recorded here only, **subject to** "system", "state machine" and "behavior tree" being defined. No normative file contains it.

## "automaton" replaced by "state machine" in the definitions, 2026-11-10 (later)

Asked how to handle the word "automaton", on which the accepted "state" wording depends. The owner chose **replace it with "state machine"** (recommendation followed): the standard's definitions use "state machine", which the document kinds already use; "automaton" stays as the mapping term in the ontology notes only.

- **Decided (direction):** no term "automaton" in the standard's definitions. The accepted wording of **state** is therefore reopened: it is to say "control mode of a state machine", and **state machine** needs a definition. Neither new wording is drafted or accepted yet.
- **Status of "state":** the accepted wording above stands only until the revised wording is accepted.

## Draft wording for "state" (revised) and "state machine" chosen, 2026-11-10 (later)

Asked whether to take forward a pair: "state" with "automaton" replaced, and a new draft for "state machine". The owner chose the **pair as offered (recommended option, with the initial-state wording included)**. Chosen drafts, **not yet accepted as final**:

> **state**: control mode of a state machine, declared by a capability specification, in which an executor performs the behavior that the kind of the state prescribes.
>
> NOTE 1  A state is not the condition of a system or of its environment (system state), and is not the status returned by a behavior-tree node.
>
> NOTE 2  The kinds of state are defined in the requirements class for capability specifications. *(Kinds not yet decided.)*
>
> **state machine**: behavior defined as a set of states and the transitions between them, of which exactly one state is active at the start of a run, and which ends in a terminal state.
>
> NOTE  A state machine is one of the two kinds of behavior a capability specification can define; the other is a behavior tree.

**Flagged by the Architect:** the phrase "exactly one state is active at the start of a run" is **the Architect's guess**; the owner never decided an initial-state rule, and it may conflict with nested or parallel states (undecided). The owner chose the offer that includes it, so it stands here as a draft, to be confirmed or removed when accepting.

- **Not decided (still open):** acceptance of both wordings; "transition" and "terminal state" definitions (the latter now has three endings); the initial-state rule; nested and parallel states; the ontology wording.

## "state" and "state machine" wordings accepted for now, 2026-11-10 (later)

The owner chose **accept, without the guessed phrase** (recommendation followed). Accepted wording, recorded here only (no normative file contains it); it replaces the earlier accepted "state" wording that used "automaton":

> **state**: control mode of a state machine, declared by a capability specification, in which an executor performs the behavior that the kind of the state prescribes.
>
> NOTE 1  A state is not the condition of a system or of its environment (system state), and is not the status returned by a behavior-tree node.
>
> NOTE 2  The kinds of state are defined in the requirements class for capability specifications. *(Kinds not yet decided.)*
>
> **state machine**: behavior defined as a set of states and the transitions between them, which ends in a terminal state.
>
> NOTE  A state machine is one of the two kinds of behavior a capability specification can define; the other is a behavior tree.

The phrase "of which exactly one state is active at the start of a run" is **removed**; the initial-state rule is still open. Accepted **subject to** "transition", "terminal state" and "behavior tree" being defined (the first two are used here but not yet defined); the wording comes back to the owner if one of them changes.

**Accepted definitions so far (all recorded in this file only):** capability specification, executor, state, state machine. **Not yet drafted:** behavior tree, capability binding, transition, terminal state (three endings), postcondition, observation, bare "capability", halt action, authority and delegation terms.

## Third ending named "halted", 2026-11-10 (later)

Asked what to call the third ending (a run stopped from outside whose halt clean-up completed). The owner chose **halted** (recommendation followed; alternatives were "cancelled" and "stopped"). The three endings are **succeed, fail, halted**. Reason given: the action and its ending share the word "halt".

- **Risks noted:** BehaviorTree.CPP uses "halt" for resetting a node to idle with no recorded ending; the Connected Systems API's matching status is CANCELED, so the standard has to state the mapping.
- **Not decided (still open):** the exact identifier or spelling of the ending as it appears in documents (the earlier example type names are `succeed` and `fail`; whether the third is `halted` or `halt` is not decided); the definition wording; the CS API mapping. Nothing normative is drafted.

## Draft wording for "terminal state" chosen, 2026-11-10 (later)

Asked whether to take forward a draft for **terminal state** with the three endings. The owner chose the **draft with Notes 1 to 3** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **terminal state**: state in which a run of a state machine ends, and from which no transition leaves.
>
> NOTE 1  A terminal state has one ending: succeed, fail or halted.
>
> NOTE 2  Halted is reached only by a halt that has completed the exit actions of the active states; a halt whose exit actions fail or overrun ends in fail.
>
> NOTE 3  Whether a halted or failed run may be restarted is not defined here.

- **Flagged by the Architect:** the definition uses the word "run", which is not yet defined; "transition" is also undefined; Note 2 repeats a requirement-like rule inside a note (the halt decisions above), so it may need moving to the requirements when they are drafted.
- **Not decided (still open):** acceptance; "run"; "transition"; ending identifiers as they appear in documents; the restart question.

## "terminal state" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** for the **terminal state** draft with Notes 1 to 3 (recommendation followed). Accepted wording, recorded here only, **subject to** "run" and "transition" being defined, and coming back to the owner if either changes or if Note 2 moves into a requirement. No normative file contains it.

**Accepted definitions so far (this file only):** capability specification, executor, state, state machine, terminal state. **Not yet drafted:** transition, run, behavior tree, capability binding, postcondition, observation, bare "capability", halt action, authority and delegation terms.

## Draft wording for "transition" chosen, 2026-11-10 (later)

Asked which draft to take forward for **transition**. The owner chose **draft A, followed when its condition holds** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **transition**: directed connection from a source state to a target state of a state machine that the executor follows when a condition holds.
>
> NOTE 1  The condition is an expression in the language required by this standard for conditions (CEL).
>
> NOTE 2  Leaving the source state runs its exit actions, and entering the target state runs its entry actions. *(Order not decided.)*

- **Flagged by the Architect:** the definition says every transition has a condition; whether a transition may be unconditional (for example, on completion of a state's behavior) was not decided. Note 2 states a rule inside a note and uses "runs", whose order relative to the transition and to the invariant check on entry is not decided. A transition named as the response to a broken invariant is not stated in the wording.
- **Not decided (still open):** acceptance; unconditional transitions; events versus conditions as triggers; ordering of exit actions, the transition and entry actions; the "run" definition.

## "transition" wording accepted for now, 2026-11-10 (later)

The owner chose **accept without Note 2** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **transition**: directed connection from a source state to a target state of a state machine that the executor follows when a condition holds.
>
> NOTE  The condition is an expression in the language required by this standard for conditions (CEL).

Exit and entry action behavior on a transition is left to the requirements. **Still open:** whether a transition may be unconditional (if so, this wording is reopened); events versus conditions as triggers; ordering of exit actions, the transition and entry actions.

**Accepted definitions so far (this file only):** capability specification, executor, state, state machine, terminal state, transition. **Not yet drafted:** run, behavior tree, capability binding, postcondition, observation, bare "capability", halt action, authority and delegation terms.

## Draft wording for "run" chosen, 2026-11-10 (later)

Asked which draft to take forward for **run**. The owner chose **draft A, one execution from start to ending** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **run**: one execution of a capability specification by an executor, from its start until it reaches an ending.
>
> NOTE  An ending is succeed, fail or halted for a state machine. *(The endings of a behavior tree are not decided.)*

- **Not decided (still open):** acceptance; what starts a run; whether a run can be paused, resumed or restarted; the endings of a behavior tree (the bracketed part of the note is not wording); what a run record contains (ties to the provenance requirement and the open execution-record contents).

## "run" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** for **run** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **run**: one execution of a capability specification by an executor, from its start until it reaches an ending.
>
> NOTE  An ending is succeed, fail or halted for a state machine.

The behavior-tree reminder stays in this record only. **Still open:** the endings of a behavior tree; what starts a run; pause, resume and restart.

**Accepted definitions so far (this file only):** capability specification, executor, state, state machine, terminal state, transition, run. **Not yet drafted:** behavior tree, capability binding, postcondition, observation, bare "capability", halt action, authority and delegation terms. Every word used in the accepted definitions is now defined except "behavior tree" (used in capability specification, executor, state and the state machine note) and "system".

## Draft wording for "behavior tree" chosen, 2026-11-10 (later)

Asked which draft to take forward for **behavior tree** (decision 4.6: document-level shape only; no node semantics). The owner chose **draft A, rooted tree of nodes returning a status** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **behavior tree**: behavior defined as a rooted tree of nodes, each of which returns a status when the executor evaluates it.
>
> NOTE  The node types, the statuses and the rules for evaluating a tree are not defined by this standard.

**Flagged by the Architect:** the note says these are "not defined by this standard", which is stronger than the record supports. The behavior-tree dialect is **open** (an earlier answer says a dialect, if the standard has one, is the owner's to write; decision 4.6 gives document-level shape only). As normative text the note would rule a dialect out. The bracketed "dialect not decided" in the offer was a reminder, not wording.

- **Not decided (still open):** acceptance; whether the note stays, is reworded to "not yet defined", or is dropped; the dialect; the endings of a behavior tree; halting a behavior tree.

## "behavior tree" wording accepted for now, 2026-11-10 (later)

The owner chose **accept the definition, drop the note** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **behavior tree**: behavior defined as a rooted tree of nodes, each of which returns a status when the executor evaluates it.

The behavior-tree dialect (node types, statuses, evaluation rules), the endings of a behavior tree and halting a behavior tree **remain open**; the definition rules none of them out.

**Accepted definitions so far (this file only):** capability specification, executor, state, state machine, terminal state, transition, run, behavior tree. **Not yet drafted:** system, capability binding, postcondition, observation, bare "capability", halt action, authority and delegation terms. Words used in accepted definitions and still undefined: "system" (in executor), "behavior" (used throughout), "condition" (transition), "status" (behavior tree).

## Draft wording for "capability binding" chosen, 2026-11-10 (later)

Asked which draft to take forward for **capability binding** (decisions 3.4 and 4.3, and the kept requirement that a specification names its stream resources symbolically). The owner chose **draft A, ties a specification to a system by mapping names** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **capability binding**: document that references a capability specification and ties it to a particular system by mapping the resources that the specification names symbolically to resources of that system.
>
> NOTE  A capability specification is not tied to a particular system; a capability binding ties it to one.

**Flagged by the Architect:** the mapping of symbolic names to a system's resources is the Architect's **inference** from two earlier answers; the owner never stated it in these words. The word "system" is not yet defined.

- **Not decided (still open):** acceptance; whether the mapping is the whole of what a binding does (for example, whether it also carries the halt contract for a control stream, which the research placed in the binding and the owner's decisions placed in the specification); how the reference to the specification is resolved; the kind of "resources" (Connected Systems API resources are the working assumption, not recorded as decided).

## "capability binding" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** for draft A of **capability binding** (recommendation followed), which also **confirms the mapping of symbolic names to a system's resources** as part of what a binding is. Accepted wording, recorded here only (no normative file contains it), **subject to** "system" being defined:

> **capability binding**: document that references a capability specification and ties it to a particular system by mapping the resources that the specification names symbolically to resources of that system.
>
> NOTE  A capability specification is not tied to a particular system; a capability binding ties it to one.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, state, state machine, terminal state, transition, run, behavior tree. **Not yet drafted:** system, behavior, condition, status, postcondition, observation, bare "capability", halt action, authority and delegation terms.

## Draft wording for "system" chosen, 2026-11-10 (later)

Asked which draft to take forward for **system** (decision 3.1; working approach: SOSA/SSN `System`). The owner chose **draft A, adopt the SOSA/SSN term by reference** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **system**: system as defined in SOSA/SSN [W3C SOSA/SSN, 2017].
>
> NOTE 1  Software and virtual systems are systems.
>
> NOTE 2  A system may have other systems as components.

**Checked by the Architect against the pinned text** (W3C SOSA/SSN Recommendation, 2017-10-19, `https://www.w3.org/TR/2017/REC-vocab-ssn-20171019/`, section 4.9.2.4, fetched 2026-11-10): `ssn:System` (IRI `http://www.w3.org/ns/ssn/System`) is defined as "a unit of abstraction for pieces of infrastructure that implement Procedures. A System may have components, its subsystems, which are other Systems." So Note 2 matches the source. For Note 1, the Recommendation's introductory text says the new SSN and SOSA "address this issue by allowing all major classes to be virtual" (virtual sensors, including software and simulations); the section 4.9.2.4 definition itself does not mention software. Note 1 is therefore the owner's decision 3.1, supported by that introductory text, not a statement made by the System definition. The term is `ssn:System`; `sosa:System` is the 2023 draft's IRI, per the ontology notes.

- **Not decided (still open):** acceptance; whether "system as defined in SOSA/SSN" should name the class `ssn:System` explicitly; the precise citation form; the 2023 draft's differences (informative only).

## "system" wording accepted for now, 2026-11-10 (later)

The owner chose **accept, naming `ssn:System`** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **system**: system, as defined by `ssn:System` in SOSA/SSN [W3C SOSA/SSN, 2017].
>
> NOTE 1  Software and virtual systems are systems.
>
> NOTE 2  A system may have other systems as components.

Note 1 is the owner's decision 3.1, not a statement of the cited definition. This closes the dependency of **executor** and **capability binding** on an undefined "system".

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree. **Not yet drafted:** behavior, condition, status, postcondition, observation, bare "capability", halt action, authority and delegation terms.

## Draft wording for "behavior" chosen, 2026-11-10 (later)

Asked which draft to take forward for **behavior**. The owner chose **draft A, what a specification defines and an executor performs** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **behavior**: what a capability specification defines and an executor performs.

**Flagged by the Architect (found after the offer was made):**
- **Circularity.** The accepted wording of *capability specification* is "document that defines a behavior", and this draft defines behavior as "what a capability specification defines". Each term is explained by the other, so neither tells a reader anything new. The Architect should have flagged this in the offer. The same applies to *run*, *state* and *executor* only indirectly (they rely on "behavior" and "capability specification"), but the pair is circular as it stands.
- **The ontology note** shown in the offer ("a behavior is information carried by the executing system") was the owner's working approach, not drafted wording, and sits uneasily next to "performs".

- **Not decided (still open):** acceptance; how to break the circle (define behavior independently, or reword capability specification so it does not use "behavior", or accept a primitive term and say so); the ontology wording.

## "behavior": research requested before any wording, 2026-11-10 (later)

Asked which of two independent wordings for **behavior** to take forward (A: responds to observations to achieve an outcome; B: actions and the decisions that select them). The owner chose **neither**, and asked for **a deep recon research agent to identify the best definition for behavior, given the literature of autonomy and independent verification and validation (IV&V) assessments**.

- **Decided:** no wording for *behavior* is proposed or accepted until the research is in. The circularity with *capability specification* (see above) stays unresolved until then; the earlier choice to "give behavior its own meaning" stands as the direction.
- **Status of dependent wording:** the accepted definitions that use the word "behavior" (capability specification, executor, state, state machine, behavior tree) are unchanged, and are accepted **subject to** this term being defined.
- **Research brief (to be run):** read-only public sources; put no project information in requests; write one report under `_bmad-output/`; do not commit.

## "behavior" research delivered, 2026-11-10 (later)

The research the owner asked for is in `_bmad-output/research-behavior-definition/research-behavior-definition.md` (agent-written, git-ignored; digests and a memlog sit beside it). Not yet reviewed by the owner. Three rounds of public-source reading (standards and IV&V bodies; formal methods and robotics; ontologies); claims are evidence-tagged. **No wording for "behavior" is chosen or accepted.**

- **Findings that matter for the choice:** the literature uses "behavior" in two opposite senses, specified (UML 2.5.1: "a specification of events that may occur dynamically over time"; ISO/IEC 10746-2) and performed (Lamport: a sequence of states; IEEE 982:2024: "observable sequence of inputs and outputs"); the sources avoid circularity by fixing which side the word names. **CCO 2.2 has a class Behavior (`ont00001347`) and it is an occurrent (an Act)**, opposite to the owner's working approach (behavior as information); an earlier research line that said CCO had no such class was wrong. The report ranks four candidate wordings; rank 1 is the specified-side wording, which leaves all accepted definitions unchanged.
- **Gaps stated in the report:** ISO 8373, SAE J3016, IEEE 1872 and 1012, IEC 61508, ISO 26262, ISO 21448, the DoDD 3000.09 glossary, NASA IV&V guidance, SysML v2, SOMA, UFO-B were not read.
- **Open:** which wording, if any, the owner takes; the ontology notes (`docs/ontology/autonomy-ontology-notes.md`) do not yet mention CCO's Behavior class.

## "behavior": specified side chosen, 2026-11-10 (later)

Asked which side of the specified/performed split "behavior" should name. The owner chose **the specified side, UML-style** (recommendation followed): behavior is the specification of what a system may do over time and when; the performed thing stays "run". The report's rank-1 wording is the starting draft; it is **not yet accepted**.

- **Decided (direction):** "behavior" names the specified thing, independent of "capability specification". The accepted definitions that use the word are unchanged.
- **Consequences noted:** nothing observable attaches to "behavior" itself, so tests attach to a *run* (its trace checked against the behavior); the ontology must map the standard's "behavior" to CCO's Plan, Algorithm or Performance Specification family and the standard's "run" to CCO's Act, not "behavior" to CCO's Behavior class (an occurrent), and this collision is to be documented.
- **Not decided (still open):** the exact wording; whether "run" gains a note about its observable trace; whether the redundancy "a document that defines a (specification)" in *capability specification* is acceptable.

## Draft wording for "behavior" chosen, 2026-11-10 (later)

The owner chose to take **the draft with both notes** forward (recommendation followed). Chosen draft, **not yet accepted as final**:

> **behavior**: specification of the actions that a system may take over time, and of the conditions that govern when they may occur.
>
> NOTE 1  An executor carries out a behavior in a run; the observable sequence of actions and observations during a run is not itself the behavior.
>
> NOTE 2  *(Informative, for the ontology notes, not the standard's text.)* Not the same as the class Behavior in the Common Core Ontologies, which is an occurrent.

**Flagged by the Architect:** Note 2 is a remark about another ontology and the offer itself labelled it "not the standard's text"; it does not belong in a definition and should live in `docs/ontology/autonomy-ontology-notes.md`. Sources for the wording: OMG UML 2.5.1 13.4.2.1; ISO/IEC 10746-2:2009 8.7 (via IEEE SEVOCAB). The word "run" in Note 1 relies on the accepted definition of *run*; "conditions" is not yet defined.

- **Not decided (still open):** acceptance; where Note 2 goes; whether "conditions" needs its own definition (it is also used in *transition* and the postcondition and invariant decisions).

## "behavior" wording accepted for now, 2026-11-10 (later)

The owner chose **accept definition and Note 1; Note 2 to the ontology notes** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **behavior**: specification of the actions that a system may take over time, and of the conditions that govern when they may occur.
>
> NOTE  An executor carries out a behavior in a run; the observable sequence of actions and observations during a run is not itself the behavior.

Note 2 (the Common Core Ontologies' class Behavior is an occurrent, not the same thing) is **not part of the standard's text**. It is to be carried by `docs/ontology/autonomy-ontology-notes.md`; **that file has not been edited yet** (the Architect did not take the choice as a request to edit it, and will do so only if asked).

This removes the circularity with *capability specification*. **Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior. **Not yet drafted:** condition, status, postcondition, observation, bare "capability", halt action, authority and delegation terms. "condition" is now used in *behavior* and *transition* and is undefined.

## Draft wording for "condition" chosen, 2026-11-10 (later)

Asked which draft to take forward for **condition** (used in *behavior* and *transition*). The owner chose **draft B, true-or-false expression** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **condition**: expression, in the language required by this standard for conditions, that evaluates to true or false.
>
> NOTE  A condition holds when it evaluates to true.

**Flagged by the Architect (after the offer):** the phrase "in the language required by this standard for conditions" is **self-referential**, since it defines "condition" through "conditions". The CEL decision allows naming the language directly (CEL, pinned release `v0.26.0`, a normative reference). Also, a CEL expression can fail to evaluate (error or missing value); how that counts is **not decided** here (the "no data counts as broken" rule covers only invariants).

- **Not decided (still open):** acceptance; naming CEL directly; evaluation failures; what a transition's condition may read (the "over observations" rule is for postconditions and invariants only).

## "condition" wording accepted for now, 2026-11-10 (later)

The owner chose **accept, naming CEL directly** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **condition**: expression in CEL that evaluates to true or false.
>
> NOTE  A condition holds when it evaluates to true.

CEL is the owner's chosen language and a normative reference (pin: `v0.26.0`, commit `21ec6f4e52e8d694687ff9ed7408d3eccbb955d7`); the definition cites it, it does not add a decision. **Knock-on for earlier wording (not changed, for the owner to decide):** the accepted *transition* note says "The condition is an expression in the language required by this standard for conditions (CEL)", which now repeats the definition; it can be shortened or dropped when the wording is next reviewed.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition. **Not yet drafted:** status, postcondition, observation, bare "capability", halt action, authority and delegation terms. **Still open for *condition*:** what happens when a CEL expression fails to evaluate (error or missing value), beyond the invariant "no data counts as broken" rule.

## Draft wording for "observation" chosen, 2026-11-10 (later)

Asked which draft to take forward for **observation** (decisions 3.7 and the invariant and postcondition decisions). The owner chose **draft A, adopt SOSA/SSN by reference** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **observation**: observation as defined by `sosa:Observation` in SOSA/SSN [W3C SOSA/SSN, 2017].
>
> NOTE  A condition reads the results of observations.

**Checked by the Architect against the pinned text** (W3C SOSA/SSN Recommendation, 2017-10-19, `https://www.w3.org/TR/2017/REC-vocab-ssn-20171019/`, fetched 2026-11-10): `sosa:Observation` is "Act of carrying out an (Observation) Procedure to estimate or calculate a value of a property of a FeatureOfInterest." `sosa:Result` is "The Result of an Observation, Actuation, or act of Sampling. To store an observation's simple result value one can use the hasSimpleResult property." `sosa:hasResult` links an Observation to a Result "which contains a value representing the value associated with the observed Property". So the Note's "results of observations" matches SOSA's own terms, and the Observation itself is an act (occurrent), the Result is what a condition reads.

- **Not decided (still open):** acceptance; whether "a new observation arrives" (invariant timing) means a new result; time of an observation (when the value applies, when produced); the stale-data rule; ordering and batching; the use of SOSA's Result versus the Connected Systems API's observation resource and SWE Common's data record in the encodings.

## "observation" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it), **subject to** SOSA/SSN 2017 remaining the pin:

> **observation**: observation as defined by `sosa:Observation` in SOSA/SSN [W3C SOSA/SSN, 2017].
>
> NOTE  A condition reads the results of observations.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation. **Not yet drafted:** status, postcondition, bare "capability", halt action, authority and delegation terms, invariant. **Still open:** timing of observations; the stale-data rule; what "a new observation arrives" means (a new result, by the check above).

## Draft wording for "postcondition" chosen, 2026-11-10 (later)

Asked which draft to take forward for **postcondition** (decision 3.7: a condition over observations). The owner chose **draft B, condition over observations, meaning left to requirements** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **postcondition**: condition that reads observations.
>
> NOTE  What a postcondition is declared for, and when it is evaluated, are specified in the requirements class for capability specifications.

**Flagged by the Architect:** the wording gives no sense of "post" (after something), so it does not separate a postcondition from any other condition that reads observations (an invariant, a transition's condition might read them too); the distinction is carried only by the requirements. Earlier notes (not decisions): command nodes in a behavior tree carry a postcondition; a separate "intended effect" idea may be added later; a postcondition time limit was dropped.

- **Not decided (still open):** acceptance; what a postcondition is declared for; when it is evaluated; its relation to the endings (succeed, fail, halted).

## "postcondition" wording accepted for now, 2026-11-10 (later)

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **postcondition**: condition that reads observations.
>
> NOTE  What a postcondition is declared for, and when it is evaluated, are specified in the requirements class for capability specifications.

The wording comes back to the owner if the requirements need the definition to say more.

## Draft wording for "invariant" chosen, 2026-11-10 (later)

Asked which draft to take forward for **invariant** (the invariant decisions above). The owner chose **draft A, condition that must hold while a state is active** (recommendation followed). Chosen draft, **not yet accepted as final**:

> **invariant**: condition, declared for a state, that reads observations and that is required to hold while the state is active.
>
> NOTE  When an invariant is evaluated, what a broken invariant causes, and the response that every invariant declares are specified in the requirements class for capability specifications.

**Flagged by the Architect:** (1) the term name is **not decided**; the owner's design question said "mode invariants", and the draft uses "invariant" (a state, not a "mode", is the accepted term, so "invariant" follows the accepted vocabulary). (2) "is required to hold" puts a requirement-like statement inside a definition. (3) The Note says what a broken invariant "causes", while the decision is that each invariant declares its own response; the wording matches the decision only loosely.

- **Not decided (still open):** acceptance; the term name; the list of permitted responses.

## "invariant" wording accepted for now, 2026-11-10 (later)

The owner chose **accept, with the note reworded** (recommendation followed). Accepted wording, recorded here only (no normative file contains it); it also accepts **"invariant" as the standard's term** (not "mode invariant"):

> **invariant**: condition, declared for a state, that reads observations and that is required to hold while the state is active.
>
> NOTE  When an invariant is evaluated, and the response that every invariant declares to its being broken, are specified in the requirements class for capability specifications.

"is required to hold" stays in the definition as accepted; the Architect's flag about it being rule-like is noted, not resolved.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant. **Not yet drafted:** status, bare "capability", halt action, authority and delegation terms, entry action and exit action, the three endings as terms (succeed, fail, halted), action.

## JPL Autonomica paper listed as an informative reference, 2026-11-10 (later)

The owner asked for a comparison of the JPL paper *Autonomica: Ontological Modeling and Analysis of Autonomous Behavior* (Elaasar et al., INCOSE International Symposium 2023, DOI 10.1002/iis2.13099) with the work so far, and then said: **list it as an informative reference**. It is listed in `docs/references/README.md` under "Informative references", by DOI and URL only. The PDF is **not stored** in the repository: the copy read says "Permission granted to INCOSE to publish and use" and states no open licence. Nothing normative depends on it, and no gate or pin changed.

What the comparison found (research summary and comparison note in the git-ignored `_bmad-output/research-candela-autonomica-incose-2023-paper/`; the owner's verdict: it added little, and neither of the two points below worries them):
- The paper never defines "behavior", "capability", "state" or "specification"; it defines only "autonomy" (taken from Fong et al. 2018). It has no halt, authority, delegation or IV&V content and no upper-ontology alignment.
- Its pre, maintenance and post conditions on a task line up with this standard's transition conditions, invariants and postconditions. It uses "state" for the condition of the physical system, the sense the accepted "state" Note 1 excludes.
- Points kept for later drafting, no decision: the paper uses "capability" for an invocable function, not a document (relevant to the open question of bare "capability"); it uses "action" for something done to the controlled system (relevant when "action" is drafted); it covers planning and replanning, which nothing accepted covers (a scope statement may be wanted); whether a condition may read an estimate rather than a raw observation sits with the open stale-data rule.

**Accepted definitions so far (this file only):** unchanged (fifteen). **Not yet drafted:** status, bare "capability", halt action, authority and delegation terms, entry action and exit action, the three endings as terms (succeed, fail, halted), action.

## Draft wording for "action" chosen, 2026-11-11

Asked which draft to take forward for **action**. The owner chose **draft A, operation the executor performs as directed** (recommendation followed; the alternatives were an operation on a named resource, and leaving the word undefined). Chosen draft, **not yet accepted as final**. The Architect adjusted the Note from what the card described: it now says the executor performs the action (the point about the JPL paper's different use), and it no longer names the halt action (see the flag below):

> **action**: operation that an executor performs as directed by a capability specification.
>
> NOTE  An action is performed by the executor. Sending a command to a system is an action, and so are the entry actions and exit actions of a state.

**Flagged by the Architect:** (1) "operation" is itself undefined; it is used in its ordinary sense. (2) The halt action is left out of the Note on purpose: who may issue a halt is still open, and a halt issued from outside the specification is a request, not an action the specification directs, so naming it here could settle that by accident. (3) Entry actions and exit actions are not yet defined as terms; the Note uses them in their plain sense. (4) The JPL paper uses "action" for something done to the controlled system (a different sense); the Note's first sentence is the guard against that reading.

- **Not decided (still open):** acceptance; whether the halt action is an action in this sense; what an action may act on (left to the requirements).

## "action" wording accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **action**: operation that an executor performs as directed by a capability specification.
>
> NOTE  An action is performed by the executor. Sending a command to a system is an action, and so are the entry actions and exit actions of a state.

The halt action is not named in the Note; whether it is an action in this sense stays open with the question of who may issue a halt.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action (sixteen). **Not yet drafted:** status, bare "capability", halt action, authority and delegation terms, entry action and exit action, the three endings as terms (succeed, fail, halted).

## Draft wording for "entry action" and "exit action" chosen, 2026-11-11

Asked which draft to take forward for **entry action** and **exit action**. The owner chose **draft A, two short definitions with the halt link in the Note** (recommendation followed; the alternatives were the same pair without the halt Note, and a single term "state action"). Chosen draft, **not yet accepted as final**:

> **entry action**: action that an executor performs when it enters a state.
>
> **exit action**: action that an executor performs when it leaves a state.
>
> NOTE  The exit actions of the active states are the clean-up when a run is halted.

**Flagged by the Architect:** (1) The Note restates the halt decision (clean-up is the exit actions of the active states; a failed or overrunning clean-up ends in fail). If the halt design changes, the Note changes. (2) The Note is attached to "exit action" only; entry actions have no halt role. (3) Nothing here says which actions a state declares or in what order they run; both are left to the requirements class for capability specifications. (4) "Leaves a state" covers leaving by a transition and leaving because of a halt; the draft does not distinguish them. (5) Nested or parallel states are still undecided, so "the active states" (plural) in the Note presumes that more than one state can be active at once; that follows the earlier halt decision, but is not settled.

- **Not decided (still open):** acceptance; ordering and timing of actions; whether more than one state can be active at once.

## "entry action" and "exit action" wording accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **entry action**: action that an executor performs when it enters a state.
>
> **exit action**: action that an executor performs when it leaves a state.
>
> NOTE  The exit actions of the active states are the clean-up when a run is halted.

The plural "active states" stays as the halt decision had it; whether more than one state can be active at once (nested or parallel states) remains open.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action, entry action, exit action (eighteen). **Not yet drafted:** status, bare "capability", halt action, authority and delegation terms, the three endings as terms (succeed, fail, halted).

## Draft wording for "ending" chosen, 2026-11-11

Asked which draft to take forward for the three endings (succeed, fail, halted). The owner chose **draft A, one term "ending" with the three meanings in a Note** (recommendation followed; the alternatives were four terms, and leaving "ending" undefined). The reason for one term: "succeed" and "fail" are also two of the six state types in the examples, which are to become kinds of state, so defining them here as terms would give one word to an ending and a kind of state. Chosen draft, **not yet accepted as final**:

> **ending**: outcome of a run, which is one of succeed, fail or halted.
>
> NOTE  A run ends in succeed when it has completed the behavior, in fail when it could not, and in halted when a halt stopped it and the clean-up completed.

**Flagged by the Architect:** (1) "completed the behavior" and "could not" are loose; what counts as completing is left to the requirements (which terminal states are declared as which ending). (2) The Note says "a halt", and the halt action is not yet defined. (3) A halt whose clean-up fails or overruns ends in fail; the Note's "in fail when it could not" covers that only loosely, and the exact rule is in the accepted "terminal state" Note 2. (4) Endings are defined for state machines only (the accepted "run" Note); the behavior-tree endings are deferred with the behavior-tree halting question. (5) How a document names an ending (identifiers) is still open. (6) The words "succeed", "fail" and "halted" stay free for other uses, such as kinds of state.

- **Not decided (still open):** acceptance; behavior-tree endings; ending identifiers in documents.

## "ending" wording accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **ending**: outcome of a run, which is one of succeed, fail or halted.
>
> NOTE  A run ends in succeed when it has completed the behavior, in fail when it could not, and in halted when a halt stopped it and the clean-up completed.

"succeed", "fail" and "halted" are not separate terms. The Note's use of "halt" depends on the halt action, which is drafted next and may send the Note back to the owner.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action, entry action, exit action, ending (nineteen). **Not yet drafted:** status, bare "capability", halt action, authority and delegation terms.

## Draft wording for "halt" chosen, 2026-11-11

Asked which draft to take forward for the halt (the owner's "explicit halt action" decision above). The owner chose **draft A, define "halt" as an instruction from outside** (recommendation followed; the alternatives were defining "halt action" as an action, and leaving the halt undefined). Reason: the accepted "action" is performed by the executor as directed by a capability specification, while a halt arrives from outside and the executor responds to it, so calling it an action would pull against the accepted wording. Chosen draft, **not yet accepted as final**:

> **halt**: instruction, issued to an executor from outside a run, that the run stop.
>
> NOTE  On a halt, the executor leaves the active states, performing their exit actions; the run ends in halted if that completes, and in fail if it does not.

**Flagged by the Architect:** (1) The earlier decision says the document format has an explicit halt **action**, "a named step an authority can issue". This draft names the **halt** and does not call it an action; how a document declares or names the halt (the "explicit halt action" in the format) is left to the requirements. If the owner wants the format's construct to be called a "halt action", that name is still free. (2) Who may issue a halt is not in the wording ("from outside a run" decides nothing about authority). (3) The Note restates three earlier decisions (clean-up is the exit actions; completion gives halted; failure or overrun gives fail) and overlaps the accepted "terminal state" Note 2 and the "exit action" Note; the duplication may need removing when requirements are drafted. (4) Halting a behavior tree is deferred; the Note speaks of "active states" and so covers state machines only. (5) The clean-up time limit, a second halt arriving during clean-up, the recorded cause, and restart or resume are not in the wording. (6) The Connected Systems API cancel command and CANCELED status map to this; the mapping is still to be stated.

- **Not decided (still open):** acceptance; the name of the format's construct; who may issue a halt; the time limit; second halt; recorded cause; behavior-tree halting; the Connected Systems API mapping.

## "halt" wording accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **halt**: instruction, issued to an executor from outside a run, that the run stop.
>
> NOTE  On a halt, the executor leaves the active states, performing their exit actions; the run ends in halted if that completes, and in fail if it does not.

The accepted "ending" Note and "exit action" Note, which use "halt", now have a definition behind them. The name of the document construct (the "explicit halt action" of the earlier decision), who may issue a halt, the clean-up time limit, a second halt during clean-up, the recorded cause, restart or resume, behavior-tree halting and the Connected Systems API mapping stay open.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action, entry action, exit action, ending, halt (twenty). **Not yet drafted:** status, bare "capability", authority and delegation terms.

## Draft wording for "status" chosen, 2026-11-11

Asked which draft to take forward for **status** (the value a behavior-tree node returns). The owner chose **draft A, generic, values left to the requirements** (recommendation followed; the alternatives were the same with the common values as an example, and leaving the word undefined). Chosen draft, **not yet accepted as final**:

> **status**: value that a node of a behavior tree returns when the executor evaluates it, reporting how that evaluation went.
>
> NOTE  The values that a status can take are specified in the requirements class for capability specifications. A status is not an ending.

**Flagged by the Architect:** (1) The behavior-tree dialect (node types, status values, evaluation rules) is still open, so the values are not named; the Note defers them to a requirements class that does not exist yet. (2) "A status is not an ending" keeps a node's status apart from a run's endings (succeed, fail, halted); the words overlap in ordinary use (a node's success and a run's succeed). (3) "reporting how that evaluation went" is loose by design. (4) Behavior-tree tools differ on the value set (for example the common success, failure and running, with BehaviorTree.CPP adding more); the definition rules none of them out. (5) The accepted "state" Note 1 and "behavior tree" definition already use "status" and now have a definition behind them.

- **Not decided (still open):** acceptance; the behavior-tree dialect and its status values.

## "status" wording accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Accepted wording, recorded here only (no normative file contains it):

> **status**: value that a node of a behavior tree returns when the executor evaluates it, reporting how that evaluation went.
>
> NOTE  The values that a status can take are specified in the requirements class for capability specifications. A status is not an ending.

The status values stay open with the behavior-tree dialect.

**Accepted definitions so far (this file only):** capability specification, capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action, entry action, exit action, ending, halt, status (twenty-one). **Not yet drafted:** bare "capability", authority and delegation terms.

## Bare "capability" not defined; Note 1 of "capability specification" reworded (draft), 2026-11-11

Asked whether the standard defines the bare word "capability". The owner chose **draft A, do not define it and reword Note 1** (recommendation followed; the alternatives were defining it as the behavior, and defining it as an ability). Reasons: the Common Core Ontologies use "capability" for an ability borne by a physical thing (which the ontology notes keep as a separate notion carried by the executing system), and the JPL Autonomica paper uses it for a function one layer offers another, so defining it as the behavior would put one word on two things. Chosen draft, **not yet accepted as final**. The definition of **capability specification** keeps its accepted wording; Note 1 changes and Note 2 stays:

> **capability specification**: document that defines a behavior as a state machine or a behavior tree.
>
> NOTE 1  The standard does not define "capability" on its own; "capability specification" and "capability binding" are the names of documents.
>
> NOTE 2  A capability specification is not tied to a particular system; a capability binding ties it to one.

**Flagged by the Architect:** (1) Note 1 says what the name is not; it does not say why the name contains "capability". A reader may still ask. (2) Note 1 would also speak for "capability binding", whose own definition has no such Note; it names the term and does not change its wording. (3) The old Note 1 ("The behavior defined by a capability specification is the capability") is withdrawn, so nothing in the standard now identifies a capability with a behavior. (4) Whether the identifier's type segment becomes `capability-specification` is a separate open item and is not touched.

- **Not decided (still open):** acceptance; whether any other place in the standard will need the bare word (a later requirement may force a definition).

## Bare "capability" decision accepted for now, 2026-11-11

The owner chose **accept for now** (recommendation followed). Recorded here only (no normative file contains it). The standard does **not** define bare "capability". Accepted wording of **capability specification**, with Note 1 replaced:

> **capability specification**: document that defines a behavior as a state machine or a behavior tree.
>
> NOTE 1  The standard does not define "capability" on its own; "capability specification" and "capability binding" are the names of documents.
>
> NOTE 2  A capability specification is not tied to a particular system; a capability binding ties it to one.

This supersedes the earlier Note 1 ("The behavior defined by a capability specification is the capability"), which is withdrawn. A later requirement that needs the bare word comes back to the owner for a definition.

**Accepted definitions so far (this file only):** capability specification (with the reworded Note 1), capability binding, executor, system, state, state machine, terminal state, transition, run, behavior tree, behavior, condition, observation, postcondition, invariant, action, entry action, exit action, ending, halt, status (twenty-one). Bare "capability" is deliberately not defined. **Not yet drafted:** authority and delegation terms.

## Who may issue a halt: the standard says nothing, 2026-11-11

Asked where to start on authority and delegation. The owner chose **decide who may issue a halt first** (recommendation followed; the alternatives were leaving authority to the requirements and ontology, and drafting a small set of authority terms now). None of the twenty-one accepted definitions uses an authority word; the only live question was who may issue a halt.

Then asked who may issue a halt to an executor. The owner chose **A, the standard says nothing about who** (recommendation followed; the alternatives were that the capability binding names who may halt, and that only a party holding a stated authority may).

- **Decided:** the standard does not say who may issue a halt. Access control stays with the platform (for example the Connected Systems API's own security). The standard says only what an executor does with a halt it accepts: it runs the exit actions of the active states, then the run ends in halted, or in fail if the clean-up fails or overruns (the accepted "halt" Note).
- **Consequence:** no authority term is needed for the halt. The accepted "halt" wording ("issued to an executor from outside a run") stands unchanged.
- **Risks noted by the Architect:** (1) The standard will not say whether an executor should refuse a halt from the wrong party, so a safety reviewer may ask. (2) The choice is additive: a binding-level list of permitted parties (draft B) or an authority concept (draft C) can be added later without changing what a halt does. (3) The wider authority and delegation terms in the ontology notes (delegation within boundaries, human-authority gates, custody leases) are **not** settled by this; they remain candidates for requirements and ontology terms, to be drafted when a requirement needs one. (4) "authority" in the identifiers question (the naming authority) is a different meaning and is untouched.
- **Not decided (still open):** the clean-up time limit and how it is set; a second halt during clean-up; the recorded cause; restart or resume; behavior-tree halting; the Connected Systems API mapping; the delegation, boundary, human-authority gate and custody lease terms.

**Accepted definitions so far (this file only):** unchanged (twenty-one). **Not yet drafted:** authority and delegation terms beyond the halt, which no accepted text needs yet.

## Active states: nested only, 2026-11-12

Asked whether more than one state can be active at once. The owner chose **nested only** (recommendation followed; alternatives were one flat state at a time, and nested plus parallel).

- **Decided (direction):** a state may sit inside a parent state, so one innermost state is active together with its parents. There are no parallel sections in the first version. This fits the accepted halt wording ("the exit actions of the active states"). Parallel states remain a possible later extension.
- **Consequence for accepted wording:** the accepted **state machine** and **state** definitions do not mention parents or children; whether they need a Note is not decided.
- **Not decided (still open):** how a parent relates to its children in the documents (the name of the construct); order of exit and entry actions across parent and child (this joins the existing ordering question); which invariants apply when a child is active (a parent's invariants as well as the child's is the likely reading, not decided); the initial-state rule for a parent (which child starts); how a transition leaving a parent behaves; whether a terminal state can sit inside a parent. Nothing normative is drafted.

## Initial state: declared, one per level, 2026-11-12

Asked how a state machine says which state it starts in, now that states can nest. The owner chose **declared, one per level** (recommendation followed; alternatives were the first state listed, and chosen at run time).

- **Decided (direction):** the state machine names exactly one initial state at its top level, and every parent state names exactly one initial child. A document that omits one, or names more than one, does not conform. Nothing is inferred from list order or chosen at run time.
- **Consequence:** this is the initial-state rule that was removed from the accepted "state machine" wording as a guess (2026-11-10); it is now an owner decision, but it is recorded as a rule for the requirements, not added to the definition. Whether the definition gets a Note is not decided.
- **Not decided (still open):** the name of the field; whether the initial state of a parent may itself be a parent (the rule then applies recursively; likely yes, not confirmed); what happens on a restart (restart is still open); the nested-state questions listed under "Active states". Nothing normative is drafted.

## Order of actions on a transition: exit, enter, then check, 2026-11-12

Asked in what order exit actions, entry actions and the invariant check happen when a transition fires. The owner chose **exit, then enter, then check** (recommendation followed; alternatives were exit, check, then enter, and leaving the order to each specification).

- **Decided (direction):** on a transition, the executor runs the exit actions of the states being left, innermost first; then the entry actions of the states being entered, outermost first; and only after the entry actions have finished checks the invariants of the states now active. A parent that is neither left nor entered is untouched. This is the SCXML order (SCXML is a pinned reference).
- **Amends an earlier decision:** "Invariant checked on entry" (2026-11-10) said the check happens "before the state does anything else". It was flagged then as not confirmed. That wording is **superseded**: the check now follows the entry actions. The decision to check on entry, and the "no observation yet counts as broken" rule, stand.
- **Risk noted:** entry actions can run in a state whose invariant is already broken, and a broken invariant is then answered by its declared response. A specification that must not act in an unsafe condition has to put that guard in a transition condition, not rely on the entry check.
- **Not decided (still open):** whether exit actions of the states being left also run when a broken-invariant response is itself a transition (likely yes, the same order); what happens if an entry action fails; the interaction with the open halt details (a halt during entry actions); names and wording. Nothing normative is drafted.

## Transitions: condition required, 2026-11-12

Asked whether every transition must have a condition. The owner chose **condition required** (recommendation followed; alternatives were an optional condition meaning "on completion", and a required condition plus a built-in "completed" value).

- **Decided (direction):** every transition has a CEL condition; a document with a transition that has none does not conform. The accepted "transition" wording ("follows when a condition holds") stands unchanged.
- **Consequence:** a state whose work simply finishes needs something a condition can read to know it has finished. How a state's completion (or any observation) is exposed to a condition is **not decided** and is now a more pressing open question; it is the same question as "how observations are exposed to a condition" listed under the CEL decisions.
- **Not decided (still open):** how several transitions out of one state are ordered when more than one condition holds at once (a tie-break rule); how observations and a state's completion are exposed to conditions; when conditions are evaluated (the invariant rule is "each new observation"; transitions not decided). Nothing normative is drafted.

## Condition data follows the Connected Systems API, 2026-11-12

Asked how a condition reads the data it depends on. The three offered options were named inputs holding the latest value (recommended), the whole observation record, and leaving it to the capability binding. The owner chose **none of them as offered** and answered in their own words: **"Data has to conform to the CS API and how that data is expressed through the CS API."**

- **Decided (direction):** the data a condition reads must conform to the Connected Systems API (Parts 1 and 2, both pinned), and to how the API expresses that data. The standard does not invent its own data shape for conditions.
- **Not decided (the owner's words do not settle these; they are open, not assumed):** whether a condition sees the whole API observation (value, times, datastream) or only a named value taken from it; how names in a condition are tied to API resources; how freshness and "no observation yet" show up in that shape (the stale-data rule is still open); how a state's completion is exposed, since it is not API data (the earlier question this was meant to settle is **still open**); whether conditions may also read Part 1 static properties.
- **Not checked in this session:** which exact Connected Systems API resources and fields carry observations; that must be read from the pinned parts (the earlier fact-check report `_bmad-output/research-cs-api-fact-check.md` is the starting point) before any wording.

## Check of the CS API observation form and osh-addons drivers, 2026-11-12

The owner asked to check the actual standard and look at drivers from `osh-addons` to see how their values are expressed in the CS API. Read-only lookups of two public repositories, nothing sent.

**What was read, and its limits.**
- `opengeospatial/ogcapi-connected-systems`, default-branch clone at commit `fb858be23aa03e2b824ec50b5a97ac2c2a1d3fec` (2026-09-21): Part 2 sources (`api/part2/standard/sections/` clauses 8, 20, 21; `api/part2/openapi/schemas/json/observation.json`; example observations). **This is not the pinned edition.** The pin is v1.0 (published 2025-07-16); the clone was shallow, so whether these files changed after the pin was not checked. Quotes below must be re-read against the published Part 2 before any wording.
- `opensensorhub/osh-addons` at commit `175ec27f6e0d354edf70ecc3b33f93dee642cb4c` (2026-11-12): the MAVLink driver (`BatteryStatusOutput`), the Vaisala weather driver (`VaisalaWeatherPTUOutput`) and the UxS data model helper (`UxsHelper`). **The drivers do not write CS API JSON.** Each declares a SWE Common data record in Java; the OSH server (a separate repository, not read) turns it into the API form. So how a driver value ends up in an API observation is inferred from the schema text, not seen.

**Findings.**
1. **Observation (Part 2, JSON):** `id`, `datastream@id`, `resultTime` (required), `phenomenonTime` (defaults to `resultTime`), optional `samplingFeature@id`, `procedure@link`, `parameters`, and either an inline `result` or a `result@link` to external data. `result` "must be valid according to the result schema provided in the datastream metadata". The result may be a bare number (`"result": 23.5`) or a record (`"result": {"position": {...}, "angles": {...}}`).
2. **One observation can carry several properties** (clause 8: the API "does not restrict Observation resources to have a single observed property"). The datastream lists `observedProperties` (URIs) and, per format, a schema; for the SWE Common JSON format the schema is a SWE Common data component tree.
3. **Drivers:** each output is a SWE Common record whose first field is a `time` (ISO UTC timestamp), followed by value fields that carry a property definition URI and a unit, for example `level` with the BatteryLevel property and unit `%`, or `pressure` in `inHg` and temperatures in `Fah`.
4. **Observed hazards for conditions:**
   - the same property definition can appear twice in one record (Vaisala has `tempExt` and `tempInt`, both AirTemperature), so a property URI alone does not identify a value; the field name does;
   - units differ between drivers (inHg, Fahrenheit, percent), so a condition's number only means something with the declared unit;
   - missing values can arrive as `NaN` inside an observation (Vaisala), not as an absent observation, so "no observation yet" and "an observation whose value is missing" are different cases;
   - a driver puts a `time` field inside the result while the API observation also has `resultTime` and `phenomenonTime`, so there are two places a time can come from;
   - a state's completion is not API data (still open).

**Status:** findings only. Nothing is decided from them; the question of what a condition sees is asked next.

## Naming a value in a condition: datastream plus field path, 2026-11-12

After the check above, asked how a condition picks out one value. The owner chose **datastream plus field path** (recommendation followed; alternatives were the observed property URI, and letting the author use either).

- **Decided (direction):** a condition reads a value by naming a datastream and the path of a field in that datastream's result record, as the API's result schema defines the field. The observation's own times (result time, phenomenon time) are available to the condition. The value is in the unit the schema declares.
- **Not decided (still open):** how a specification's datastream names are resolved to real datastreams (the capability binding's job is the likely home, not decided); whether the condition language syntax for this is plain CEL names or a declared-inputs list; unit conversion (none assumed); how "no observation yet" and a `NaN` or missing value inside an observation appear to a condition; the stale-data rule (the times are now readable, so a rule can be written; not decided); whether a result that is a link (`result@link`) is allowed in conditions; how a state's completion is exposed (not API data; the earlier question is **still open**); whether the Part 2 text read (a 2026-09-21 clone, not the pinned edition) matches the pin. Nothing normative is drafted.

## Stale data: declared maximum age, 2026-11-12

Asked what happens when a sensor that used to report goes silent. The owner chose **declared maximum age** (recommendation followed; alternatives were the author writing freshness in the condition, and no rule yet).

- **Decided (direction):** each datastream a specification reads declares a maximum age. If the latest observation is older than that, the executor treats the input as having no observation, which the earlier rule ("invariant with no observation counts as broken") already covers for invariants. Conditions stay plain CEL with the built-in functions only; no current-time value is added to CEL.
- **Closes:** the stale-data question left open under "Invariant with no data counts as broken" (2026-11-10).
- **Not decided (still open):** the field name; how age is measured (the observation's own time, which of its two times, against the executor's clock; clock source and its accuracy); what a transition condition sees when an input is stale (likely the same as no observation; not decided); whether the maximum age is required or optional (the wording above reads as required; not confirmed); how a `NaN` or missing value inside a fresh observation is treated. Nothing normative is drafted.

## State completion: read the command status, 2026-11-12

Asked how a condition knows a state's work has finished. The owner chose **read the command status** (recommendation followed; alternatives were a standard-defined "done" value, and no completion signal in the first version).

- **Decided (direction):** completion of a state's work is not a special value. A state that sends a command to a system finishes when the command's status report from the API says so, read by a condition like any other API data. No built-in "done" is added to CEL.
- **Source seen (not the pinned edition):** in the Part 2 clone at commit `fb858be` (2026-09-21), a command status report has a required `statusCode` with codes that include PENDING, EXECUTING, COMPLETED, CANCELED, REJECTED and FAILED (only these were seen; the full list was not read), plus `executionTime`, `percentCompletion` and `message`. The exact list and wording must be re-read against the pinned v1.0 text before any wording.
- **Closes:** the "how a state's completion is exposed" question left open under the transition and observation decisions (2026-11-12).
- **Not decided (still open):** how a specification refers to a command's status (the same naming question as for datastreams: probably a control stream and the command it sent; the binding's role is not decided); what a state that sends no command uses to end (an ordinary condition on observations is assumed, not decided); how the API's CANCELED code maps to the ending "halted" (still the Connected Systems API mapping question under the halt decisions); what a state does while its command is rejected or fails (a transition condition on REJECTED or FAILED is assumed, not decided). Nothing normative is drafted.

## Name resolution: the binding resolves names, 2026-11-12

Asked who connects the names in a specification (datastreams, command status) to the real streams of one system. The owner chose **the binding resolves names** (recommendation followed; alternatives were the specification naming real streams, and leaving it to later).

- **Decided (direction):** the capability specification uses its own local names for the data it reads (with the field path and maximum age declared next to each) and for the commands it sends; the capability binding maps each local name to a real datastream or control stream of one system. This keeps the accepted "capability specification" Note 2 (not tied to a particular system) true, and the accepted "capability binding" wording (which ties a specification to a system) is its home.
- **Not decided (still open):** that a binding must supply every name a specification declares, and what a missing or mismatched one means (conformance rules); whether a binding may also override or add anything else (maximum age, for example); whether the accepted "capability binding" wording needs a Note on this; the names of the fields. Nothing normative is drafted.

## Halt clean-up limit: declared per exit action, 2026-11-12

Asked what "overruns" means in the halt rule and who sets the limit. The owner chose **declared per exit action** (recommendation followed; alternatives were one limit per specification, and a limit set by the binding or the platform).

- **Decided (direction):** each exit action declares its own time limit; a clean-up overruns when an exit action exceeds its limit, and the run then ends in fail. The standard fixes no number. A specification whose exit action omits a limit does not conform.
- **Consequence:** with nested states, exit actions run in sequence (innermost first), so the total clean-up time is the sum of their limits. The accepted "halt" and "terminal state" Notes ("fail if it does not") stand unchanged.
- **Not decided (still open):** the field name; whether the limit applies to exit actions run on an ordinary transition as well as on a halt (not decided; the wording above is about halt); whether a cap on the total can also be declared; the clock used to measure the limit; what a halt does to an entry action still running; the second halt, recorded cause, restart, behavior-tree halting and Connected Systems API mapping questions. Nothing normative is drafted.

## Second halt: ignored, 2026-11-12

Asked what an executor does when a second halt arrives during clean-up. The owner chose **ignore it; clean-up continues** (recommendation followed; alternatives were a second halt that abandons clean-up, and a rule declared by each specification).

- **Decided (direction):** a halt received while an earlier halt's clean-up is running changes nothing. The exit actions continue within their declared limits and the run ends in halted or fail as already decided.
- **Risk noted:** an operator cannot force a faster stop through the standard; the per-exit-action limits are the only backstop. The standard does not say whether the executor reports that it received the second halt.
- **Not decided (still open):** whether the second halt is recorded or reported; a halt that arrives while an entry action or a state's behavior is still running (assumed to be a first halt, not decided how it interrupts); the recorded cause, restart, behavior-tree halting and Connected Systems API mapping questions. Nothing normative is drafted.

## Recorded cause: ending plus cause, 2026-11-12

Asked whether a run must record why it ended. The owner chose **record ending plus cause** (recommendation followed; alternatives were the ending only, and leaving it to the platform).

- **Decided (direction):** every run records its ending and a cause. For fail, the cause is a reference to the invariant, exit action or command (by its name in the specification) that led to it; for halted, that a halt was issued and when. The cause is a reference to a named item, not free text.
- **Consequence:** the names of invariants, actions and commands in a specification must be unique within it, so a cause can point at one. That uniqueness rule is not yet decided.
- **Not decided (still open):** where the record is kept and its format (the Connected Systems API's own status or observation is a likely home; not decided); how it ties to PROV-O (pinned; mapping not decided); whether the identity of whoever issued a halt is recorded (the standard says nothing about authority, so probably not; not decided); the cause for a fail that does not come from one of those items; restart, behavior-tree halting and the Connected Systems API mapping. Nothing normative is drafted.

## Restart: a new run starts fresh, 2026-11-12

Asked whether a run that ended in halted or fail can be restarted or resumed. The owner chose **no; a new run starts fresh** (recommendation followed; alternatives were resuming from where it halted, and leaving it undefined).

- **Decided (direction):** a run that has ended stays ended. Trying again is a new run: it begins at the declared initial state and has its own ending and cause. Nothing is carried over. Resuming from where a halt happened is a possible later extension.
- **Consequence for accepted wording:** "terminal state" Note 3 ("Whether a halted or failed run may be restarted is not defined here") is now answered; whether it is reworded or removed is not decided. The no-transition-leaves-a-terminal-state wording stands.
- **Not decided (still open):** who or what starts a new run and how (a start instruction is not defined; "halt" is, "start" is not); whether a new run may begin while the previous run's clean-up is still running (likely not; not decided); behavior-tree halting; the Connected Systems API mapping. Nothing normative is drafted.

## Ending mapping to API command status: state it, 2026-11-12

Asked how the three endings relate to the Connected Systems API command status codes. The owner chose **state the mapping** (recommendation followed; alternatives were leaving it to the binding, and not mapping).

- **Decided (direction):** the standard states that, wherever a run's outcome is reported through the API's command status, succeed is reported as COMPLETED, fail as FAILED, and halted as CANCELED.
- **Risks noted (not resolved):** (1) the API text read defines CANCELED as cancellation "by an authorized user", while the standard says nothing about who may halt, so a halt issued by the platform itself may not fit the API's own reading; (2) the mapping applies only when a run is reported as a command, which depends on a decision not yet made (how a run is started and reported); (3) the text read was a 2026-09-21 clone, not the pinned v1.0; the exact codes and definitions must be re-read against the pinned text before any wording.
- **Not decided (still open):** how a run is started and reported (as a command or otherwise); the wording of the mapping; behavior-tree halting. This closes the Connected Systems API mapping question listed under the halt decisions, in outline. Nothing normative is drafted.

## Starting a run: a run is a command, 2026-11-12

Asked how a run is started and reported. The owner chose **a run is a command** (recommendation followed; alternatives were a start instruction defined by the standard, and leaving it to the platform).

- **Decided (direction):** starting a run is a command sent to the executor's control stream, naming the capability specification (and binding) to run. The command's status reports progress and the ending, using the mapping decided above (succeed as COMPLETED, fail as FAILED, halted as CANCELED). A halt is the API's cancel of that command. This makes the ending mapping apply to every run.
- **Consequences:** the executor exposes a control stream; the standard must say what the start command's parameters are. The accepted "halt" wording ("issued to an executor from outside a run") stands; "who may halt" stays with the platform. The risk noted under the mapping (CANCELED means "by an authorized user") is now live for every halt.
- **Not decided (still open):** the parameters of the start command; how a system that cannot use the API runs a specification (a wrapping binding is the assumed route; not decided); whether more than one run may be active on one executor at once; whether a new run may start while a previous run's clean-up is running; the parameters of the halt (the API's cancel); the cause record's home (the command status is now a likely place; not decided). Nothing normative is drafted.

## Start command contents: specification and binding references, 2026-11-12

Asked what the command that starts a run must contain. The owner chose **specification and binding references** (recommendation followed; alternatives were references plus declared run inputs, and the specification reference only).

- **Decided (direction):** the `parameters` of the start command name the capability specification to run and the capability binding that ties it to this system, each by a link or identifier. Nothing else is required in the first version. Run-specific inputs are a possible later extension.
- **Source seen (not the pinned edition):** in the Part 2 clone at commit `fb858be` (2026-09-21), a command has `id`, `controlstream@id`, `issueTime` and `parameters` as required properties, plus optional `samplingFeature@id`, `procedure@link`, `executionTime`, `sender` and `currentStatus`; `parameters` must be valid against the schema in the control stream metadata. Re-read against the pinned v1.0 before any wording.
- **Not decided (still open):** whether the references are links or identifiers (and in what form: the `urn:autonomyml` question is unresolved); the control stream's schema for the start command; what the executor does if a reference cannot be resolved or the binding does not supply every name the specification declares (a start-time check; not decided); whether the command's `sender` is used (the standard says nothing about authority); whether more than one run may be active on one executor; whether a new run may start during a previous run's clean-up. Nothing normative is drafted.

## One run at a time per executor, 2026-11-12

Asked whether one executor can have more than one run active at once, including a new run starting during the previous run's clean-up. The owner chose **one run at a time** (recommendation followed; alternatives were several runs allowed, and several but not during clean-up).

- **Decided (direction):** an executor has at most one active run. A start command that arrives while a run is active, including during clean-up after a halt, is rejected (the API's REJECTED status). A halt applies to the one active run. A system that must do two things at once uses two executors.
- **Not decided (still open):** whether REJECTED is the required status for that case or only the likely one (the wording is the owner's); whether a run counts as active from the start command's acceptance or from entering its first state; the start-time checks (unresolvable references; names the binding does not supply). Nothing normative is drafted.

## Kinds of state: four, no choice, 2026-11-12

Asked which kinds of state the first version defines. The examples used six types (`csapiCommandAction`, `succeed`, `fail`, `mode`, `behaviorTree`, `choice`). The owner chose **four kinds, no choice** (recommendation followed; alternatives were five kinds keeping choice, and four plus a wait kind).

- **Decided (direction):** the kinds of state are **command** (sends an API command; finishes by its status), **mode** (a parent state holding child states; may carry invariants), **behavior tree** (runs an embedded behavior tree), and **terminal** (ends the run with succeed or fail). There is no separate choice kind: a branch is several transitions with different conditions out of one state. The ending halted is never declared in a document; it is reached only by a halt.
- **Consequences:** `succeed` and `fail` stop being state types and become the two endings a terminal state can declare; the example documents will need changing to match. The accepted "state" Note 2 ("kinds not yet decided") is now answerable; whether it is reworded is not decided.
- **Risk noted:** this is the Architect's reading, not tested; a use for a choice kind not seen here (a branch that does nothing before choosing) would need an empty command state. The "wait" case is not given its own kind.
- **Not decided (still open):** the names of the kinds; how a state that only waits for a condition is written; whether a terminal state may sit inside a mode (assumed to be allowed, not decided); what a mode's invariants cover (the parent/child rules remain open); the ontology mapping of the kinds. Nothing normative is drafted.

## Start checks: check everything, reject if wrong, 2026-11-12

Asked what an executor must check before beginning a run. The owner chose **check everything, reject if wrong** (recommendation followed; alternatives were checking references only, and no checks).

- **Decided (direction):** before the run begins, the executor resolves both references in the start command and confirms that the binding supplies every name the specification declares. If anything is missing, the start command is rejected (the API's REJECTED status, with a message) and no run begins. This also settles that a binding must supply every name a specification declares (left open under "Name resolution").
- **Limit noted:** the check is against the binding's contents, not the live system; whether a named datastream actually exists or is reporting is not part of this check (not decided; the stale-data and no-observation rules cover it at run time).
- **Not decided (still open):** what else is checked at start (for example that the specification is valid against the standard, that conditions type-check in CEL; the CEL type-checking question is still open); the message or error content; whether a run counts as active from acceptance of the start command. Nothing normative is drafted.

## CEL type check: required at start, 2026-11-12

Asked whether conditions must be type-checked before a run begins. The owner chose **required at start** (recommendation followed; alternatives were recommended but not required, and checked when written only).

- **Decided (direction):** at start, the executor type-checks every condition against the types the binding's datastreams declare (their result schemas). A condition that fails the check rejects the start (REJECTED), like a missing name. This closes "whether CEL's own type checking is required before a run" (left open under the CEL decisions) and extends the start checks above.
- **Consequence:** executors need a CEL implementation that can check as well as evaluate, and the standard must say how a SWE Common result schema maps to CEL types. That mapping is a sizeable piece and is **not decided**; neither is how units are treated in the check (no conversion assumed).
- **Not decided (still open):** the schema-to-CEL type mapping; how `NaN` and missing values appear to the type check; the CEL features and extensions the check may assume (built-in only, per the CEL functions decision); what other start checks exist (specification validity). Nothing normative is drafted.

## Missing values: treated as no observation, 2026-11-12

Asked what a condition sees when a fresh observation carries a missing value (for example `NaN`, which the Vaisala driver sends inside an observation that did arrive). The owner chose **treat as no observation** (recommendation followed; alternatives were passing NaN through, and treating it as no observation for invariants only).

- **Decided (direction):** a field whose value is `NaN`, or is otherwise marked missing by its schema, counts exactly like no observation for that field. The earlier rules therefore apply: for an invariant it counts as broken and its declared response happens; stale data and never-reported data are handled the same way. One rule covers silent, never-reported and unusable data.
- **Consequence:** an author cannot read a `NaN` itself. This closes the "`NaN` or missing value inside a fresh observation" items left open under the stale-data and condition-data decisions.
- **Not decided (still open):** what counts as missing for each type the result schema allows (for example a text field, a missing-value marker in the schema); what a transition condition sees for such a field (the wording above says "no observation"; what a transition does with "no observation" is not decided; the invariant meaning, broken, is). Nothing normative is drafted.

## No data in a transition condition: not met, 2026-11-12

Asked what happens when a transition's condition reads an input with no observation (never reported, too old, or missing). The owner chose **condition is not met** (recommendation followed; alternatives were failing the run, and not met plus a way for the author to test for missing data).

- **Decided (direction):** a transition condition that reads an input with no observation is treated as not holding, so the transition is not followed and the executor stays in the state. The state's invariants, which count missing data as broken, still respond. This completes the no-data rules: invariants count it as broken; transition conditions count it as not met.
- **Risk noted:** a state waiting on a sensor that never reports waits for ever unless the author adds another transition or an invariant on that sensor. A timeout would need a way to express elapsed time, which is **not decided** (plain CEL has no current time and none was added).
- **Not decided (still open):** how a timeout is written (a time-based transition or invariant; not decided); a way for a condition to test for missing data (not added; "built-in CEL only" stands). Nothing normative is drafted.

## Timeouts: declared per state, 2026-11-12

Asked how a specification says "give up on this state after a time". The owner chose **declared per state** (recommendation followed; alternatives were an elapsed-time value in CEL, and no timeout in the first version).

- **Decided (direction):** a state may declare a time limit and the state to go to when the limit passes. The executor measures time since the state was entered. It is written beside the state, not as a CEL condition; nothing is added to CEL. The limit is optional: a state with none waits for ever by design.
- **Reopens accepted wording:** the accepted "transition" says a transition is followed "when a condition holds", and the decision "Transitions: condition required" says every transition has a condition. A timeout is a transition triggered by time, so the rule would become "every transition has either a condition or a time limit". The wording is **not changed**; the accepted "transition" definition comes back to the owner when it is revisited. Whether a timeout is a transition at all, or a separate construct, is not decided.
- **Not decided (still open):** the field name; whether the timeout leads to a named state or ends the run in fail; how it interacts with a state's exit actions (assumed the same order as any transition: exit, enter, check); whether it applies to a mode state (a parent whose children are active) and to the start of a run; the clock used. Nothing normative is drafted.

## Behavior trees: an optional conformance class, 2026-11-12

While preparing a question on behavior-tree halting, the Architect found a gap: behavior trees have a document shape only (decision 4.6), and the accepted "run" wording gives endings for state machines only, while later decisions assume a behavior-tree kind of state, a run as a command with ending COMPLETED, FAILED or CANCELED, and completion read from a status. With no node meanings, the standard cannot say when a behavior-tree state is finished, how a standalone behavior-tree run ends, or what a halt does to one. Asked how to handle it. The owner chose **an optional conformance class** (recommendation followed; alternatives were defining a small core dialect now, and state machines only).

- **Decided (direction):** the core standard covers state machines in full. Behavior trees go into a separate, optional conformance class: documents are checked for their shape, and an executor may claim it can run them. Node types, statuses, endings and halting for behavior trees are **not defined in the first version** and are left to that class. The "behavior tree" kind of state is available only where an executor claims the class.
- **Keeps unchanged:** decision 4.6 (document shape only) and every accepted definition. Behavior-tree halting stays deferred (as on 2026-11-10), now with a stated home.
- **Risks noted:** a claim that an executor "runs behavior trees" means little until the dialect is written; a core executor need not support one of the four kinds of state; how a state machine that contains a behavior-tree state behaves on an executor that does not claim the class (the start check rejecting it is the likely answer, not decided).
- **Not decided (still open):** what the conformance class contains and when it is written; the dialect (node types, statuses, evaluation, endings, halting); whether the start check rejects a specification using a behavior tree on an executor without the class; whether BehaviorTree.CPP and Nav2 become normative then (decision 2.2 is "informative for now, revisit"). Nothing normative is drafted.

## Invariant scope in nested states: parent's and child's both, 2026-11-12

Asked which invariants are checked while a child state inside a mode is active. The owner chose **parent's and child's both** (recommendation followed; alternatives were the child's own only, and the specification choosing per invariant).

- **Decided (direction):** while a child is active, the invariants of the child and of every parent above it are checked, each under the rules already decided (each new observation, on entry, no data counts as broken). A parent's invariant therefore covers all its children without being copied into each.
- **Consequence:** when a parent's invariant breaks, its declared response is followed from inside the child, so the permitted responses must cover that case (a transition out of the parent, or a named target); the list of permitted responses is **still undecided**. On entry to a child, the invariants of newly entered parents are checked as well (the order is the one decided: exit, enter, then check).
- **Not decided (still open):** the permitted responses; whether a parent's response leaves only the child or the whole parent (assumed to leave the parent, not decided); whether a terminal state may sit inside a mode. Nothing normative is drafted.

## Invariant response: go to a named state, 2026-11-12

Asked what an invariant's declared response may be. The owner chose **go to a named state** (recommendation followed; alternatives were a fixed list of "go to a state" or "fail the run", and a state plus actions).

- **Decided (direction):** a response names one target state, and the executor makes a transition to it in the usual order (exit, enter, then check). To end the run, the target is a terminal state with ending fail; to recover, it is a state whose entry actions do the recovery. A response carries no actions of its own. For a parent's invariant, the target is outside the parent, so the whole parent is left, children first.
- **Closes:** "the list of permitted responses" (left open under "Invariant must declare a response", 2026-11-10).
- **Consequence:** an author who wants "fail now" must declare a terminal fail state to point at. A response whose target is missing from the specification, or lies inside the state that breaks, does not conform (assumed; not decided).
- **Not decided (still open):** whether a target inside the parent that owns the invariant is allowed (assumed not); what happens if the target's own invariants are already broken on entry (a loop between states is possible; a rule against it is not decided); whether the response's transition counts as a transition for the "condition or time limit" wording (assumed it does not need one; not decided); the field name. Nothing normative is drafted.

## Postconditions: checked when the run would succeed, 2026-11-12

Asked what a postcondition is for. The owner chose **checked when the run would succeed** (recommendation followed; alternatives were a postcondition on a command state, and no separate construct).

- **Decided (direction):** a specification may declare postconditions for the whole behavior: conditions that must hold for the run to count as a success. When the run reaches a terminal state with ending succeed, the executor checks them against the observations, under the no-observation rule (no data, stale data or missing values count as broken). If any fails, the run ends in fail instead, with that postcondition as the recorded cause. This answers "what a postcondition is declared for" and "when it is evaluated", left open under the accepted "postcondition" wording; that wording stands unchanged.
- **Consequence for accepted wording:** a succeed ending is not final until the check passes. The accepted "terminal state" ("no transition leaves") and "ending" wordings may need a Note; not decided. The cause record already points at named items, so a postcondition needs a name (names must be unique; that rule is undecided).
- **Not decided (still open):** whether postconditions are optional (assumed yes); whether they are checked once, at that moment, or must hold for some time; what happens to the exit actions or any state work (the run has already reached the terminal state); how the API status reports the change from succeed to fail (the mapping gives FAILED); the field name; postconditions inside behavior-tree commands (deferred with behavior trees). Nothing normative is drafted.

## Specification contents: what the decisions imply, 2026-11-12

Asked what a capability specification must contain at minimum. The owner chose **what the decisions imply** (recommendation followed; alternatives were adding a declared interface, and deciding while drafting).

- **Decided (direction):** required: identity and version (what a start command refers to); the kind (state machine); the declared inputs (datastream, field path and maximum age) and commands under local names; and the states, with one initial state per level and a terminal state for each ending the author uses (succeed or fail). Within the states: exit-action time limits, and for each invariant a response naming a target state. Optional: postconditions, timeouts and descriptive text. No interface (what the specification offers, or reports on completion) is required in the first version.
- **Closes:** "what the document must contain" (left open when the "capability specification" wording was chosen, 2026-11-10); the accepted wording stands unchanged.
- **Risk noted:** the specification does not say what it offers to other specifications or operators, so choosing or composing specifications is left to catalogue tools outside the standard.
- **Not decided (still open):** field names; the encoding of identity and version (the `urn:autonomyml` identifier question is unresolved); whether the kind is a field or follows from the content; the contents of a capability binding (its own required list: not yet asked); the behavior-tree kind (optional class). Nothing normative is drafted.

## Binding contents: reference, system and name mappings, 2026-11-12

Asked what a capability binding must contain at minimum. The owner chose **reference, system and name mappings** (recommendation followed; alternatives were adding overrides for timing values, and deciding while drafting).

- **Decided (direction):** a binding names the specification it applies to (identity and version), the system it is for, and one mapping for every local name the specification declares (checked at start, as decided). A binding changes nothing about behavior: maximum ages, time limits, invariants and responses stay in the specification, so the specification alone decides how a run behaves. This answers "whether a binding may also override or add anything else" (left open under "Name resolution"): it may not.
- **Risk noted:** a system that is slower or faster than the specification assumes needs a different specification, not just a different binding.
- **Not decided (still open):** field names; how a mapping refers to a datastream or control stream (an API link or identifier; the same open link-or-identifier question as the start command); whether one binding may serve several versions of a specification; whether the accepted "capability binding" wording needs a Note. Nothing normative is drafted.

## Reference form: any URI the executor can resolve, 2026-11-12

Asked how a start command and a binding point at a specification (or binding). The owner chose **any URI the executor can resolve** (recommendation followed; alternatives were an API link only, and `urn:autonomyml` names only).

- **Decided (direction):** a reference is a URI (an API link, a web address, or later a registered `urn:autonomyml` name) that the executor must be able to resolve to the document, as the start check requires. The document's own identity and version must match what the reference was meant to point at. This does not depend on the URN registration; `urn:autonomyml` stays the intended scheme for the standard's own identifiers but is not required in references.
- **Closes:** "link or identifier" left open under the start command, binding contents and specification contents decisions.
- **Risk noted:** two documents at different addresses can claim the same identity and version; a mismatch rejects the start, and which copy wins is left to the platform. The mechanism for "meant to point at" (the reference carrying an expected identity and version, or only the retrieved document's own claim) is not decided.
- **Not decided (still open):** the encoding of identity and version in the document; whether the reference carries an expected identity and version; resolution rules (redirects, authentication, retrieval failure; the start check treats failure as REJECTED, assumed); the `urn:autonomyml` segment structure and the type segment (unchanged). Nothing normative is drafted.

## Identity and version: URI plus version string, 2026-11-12

Asked how a specification states its identity and version. The owner chose **URI plus version string** (recommendation followed; alternatives were a semantic version, and a version inside the URI only).

- **Decided (direction):** a specification (and a binding, by the same rule; not asked separately) has an identity, a URI, and a version, a text value, both required. The standard prescribes no numbering scheme. Two documents with the same identity and version are the same document; a changed document gets a new version.
- **Risk noted:** the standard cannot say which of two versions is newer or whether a change is compatible, and cannot test that an author changed the version when they changed the document (an identical identity and version with different content cannot be detected by the standard).
- **Not decided (still open):** whether a binding uses the same rule (assumed yes); field names; whether the reference in a start command carries an expected version (the start check compares the retrieved document's own claim with it; the mechanism is undecided); whether a binding names a specific version of its specification or a range (a binding "may serve several versions" is open). Nothing normative is drafted.

## Type mapping: every SWE Common type, with defined shapes, 2026-11-12

Asked which SWE Common types a condition can read, given that conditions are type-checked at start. The Architect recommended scalars and records. The owner **chose a different option: everything, with defined shapes**.

- **Decided (direction):** every SWE Common 3.0 component type that can appear in a result schema is mapped to a CEL type with a defined shape, so a condition may read any of them. The types seen in the schema files of the API repository clone (not checked against the pinned SWE Common 3.0 text): Boolean, Count, Quantity, Text, Category, Time, CategoryRange, CountRange, QuantityRange, TimeRange, Vector, DataRecord, DataArray, Matrix, DataChoice, DataStream, Geometry.
- **Risks noted by the Architect (not accepted or rejected by the owner beyond the choice):** this is the largest piece of the standard so far: each mapping needs rules and tests; most types are used by no decision yet; geometry needs coordinate reference system and unit rules, which the "own function set" decision deferred (built-in CEL has no geometry functions, so a geometry could be read but not meaningfully tested); `DataStream` and `Matrix` are large or block-structured and may need limits; a defined shape for `DataChoice` (which alternative is present) is an invention not in CEL.
- **Not decided (still open):** the CEL type and shape for each component type (none drafted: for example Quantity as a decimal number, Time as a CEL timestamp, a range as a pair, an array as a list, a choice as a tagged value, are the Architect's guesses, not decisions); how units and coordinate reference systems are treated in the check (no conversion assumed); the per-type missing-value markers; whether the standard defines the mapping fully or takes it by reference from a pinned SWE Common JSON schema; the order of work (all types at once, or as a table the owner reviews type by type). Nothing normative is drafted.

## Mapping work: the Architect drafts a table, the owner reviews, 2026-11-12

Asked how to work through the many type mappings. The owner chose **the Architect drafts a table; the owner reviews** (recommendation followed; alternatives were deciding type by type, and taking the mapping by reference).

- **Done:** the draft is `docs/decisions/2026-11-12-draft-swe-common-to-cel-mapping.md`. It is **proposals only, not normative, nothing accepted**. Sources: CEL `v0.26.0` at the pinned commit (read at the pin), and the SWE Common JSON schemas from the API repository clone at `fb858be` (**not the pinned SWE Common 3.0 text**).
- **Findings that change earlier assumptions:** (1) CEL's type check needs exact types, so a condition such as `level < 20` against a decimal field fails the start-time check and the author must write `20.0` (this follows from the decision to type-check at start); (2) SWE Common already defines its own missing-value markers (`nilValues`, with a reason URI) and special values (`NaN`, infinities), so "missing" has a schema-defined form per component, which answers part of the open per-type missing-marker question.
- **Not decided:** every row of the table; nine choices are listed in the draft for the owner.

## Missing values per type: NaN and declared nil values, 2026-11-12

Asked, from Choice 2 of the draft mapping table, which values count as "no observation". The owner chose **NaN and declared nil values** (recommendation followed; alternatives were adding infinities, and NaN only).

- **Decided (direction):** a value counts as no observation if it is NaN, or equals one of the component's own declared nil values (the `nilValues` list in the result schema), or, for a time, is a nil time. Infinity and minus infinity are real numbers and stay readable. This extends the earlier "missing values" decision (NaN or schema-marked) and closes the per-type missing-marker question for the simple components.
- **Consequence:** an executor reads the nil values from the result schema, not only the value. A value that equals a declared nil value is treated as no data by design.
- **Not decided (still open):** nil values for composite components (a record or array with some missing fields: whether the whole read is no observation or only that field; not decided); the other eight choices in the draft table. Nothing normative is drafted.

## Units: declared in the specification and checked at start, 2026-11-12

Asked, from Choice 3 of the draft mapping table, how units are handled in conditions. The owner chose **declare the unit in the specification** (recommendation followed; alternatives were converting automatically, and no unit check).

- **Decided (direction):** each declared input in the specification that reads a quantity also states the unit the author means. At start, the executor rejects the start (REJECTED) if the binding's datastream schema declares a different unit. No conversion is done. This extends the start checks above.
- **Consequence:** a system that reports in another unit needs a different specification or a datastream in the right unit (consistent with "a binding changes no behavior"). The standard must say how two unit references (a UCUM code or a URI) are compared; this is not decided, and the same unit can have several spellings.
- **Not decided (still open):** the comparison rule for unit references; whether a unit is required for every quantity input or only where the author states one (assumed required; not decided); units on ranges, vectors and times (a time unit is a duration unit; not decided); the field name. Nothing normative is drafted.

## Simple rows of the mapping accepted, typed from the schema, 2026-11-12

Asked, from Choice 1 of the draft mapping table, how to take the simple rows. The owner chose **accept, typed from the schema** (recommendation followed; alternatives were accepting with records checked at run time, and changing a row).

- **Decided (direction):** the rows Boolean (true or false), Count (whole number), Text (string), DataRecord (named fields) and Vector (named numbers) are accepted as drafted. The executor builds the CEL type environment from the datastream's result schema, so every field of a record or vector has its real type at start; a mistyped field name or a wrong-typed comparison is rejected at start. A type that the schema allows and the mapping does not cover is rejected at start.
- **Not decided (still open):** how the executor learns the result schema (the datastream's schema resource is assumed; not worked out); the Quantity and Time rows (Choices 4 and 5 and the Quantity detail); the remaining choices (4 to 9) in the draft table; nil values inside composites; the unit comparison rule. Nothing normative is drafted.

## Time values: a timestamp when it can be one, 2026-11-12

Asked, from Choice 5 of the draft mapping table, how a condition sees a time. The owner chose **timestamp when it can be one** (recommendation followed; alternatives were ISO date-time only, and always a number plus unit).

- **Decided (direction):** a Time is a CEL timestamp if its value is an ISO date-time, or a number with a schema-given reference time (the executor converts it). A numeric time with no reference time cannot be a timestamp, so a condition that reads it as one fails the start check. A TimeRange is a pair of timestamps. CEL's timestamp and duration arithmetic is available.
- **Source note:** the drivers read earlier send time as a number of seconds; whether their schemas give a reference time was not checked, so such a stream may be unusable in conditions as drafted. Not verified.
- **Not decided (still open):** the rule for a nil or special time (the nil-value decision covers a nil time; the special values "now" or an infinity were not read in detail); time zone handling (CEL's own rules; not compared with SWE Common); the unit rule for relative times; the other choices in the draft table (4, 6 to 9). Nothing normative is drafted.

## Arrays, matrices and streams: a declared maximum size, 2026-11-12

Asked, from Choice 7 of the draft mapping table, how to bound the reading of arrays, matrices and streams. The owner chose **the specification declares a maximum size** (recommendation followed; alternatives were one maximum fixed by the standard, and no limit).

- **Decided (direction):** each input that reads an array, matrix or stream declares the largest number of elements it will read. At start, the executor rejects the start (REJECTED) if the result schema's declared element count is larger; at run time a value that turns out larger counts as no observation. Values held out of band (a link, an external `values`) are not readable in a condition. The standard sets no number itself. DataArray, Matrix and DataStream are readable as lists of their element type, within this limit.
- **Not decided (still open):** the field name; how the size of an array with no declared element count (a variable-length array or an open stream) is judged at start (assumed: rejected unless a maximum is declared and enforced at run time; not decided); how an encoded stream block (text or binary) is decoded for reading (JSON form assumed); nested arrays (a list of lists, a matrix) and how their sizes count; the remaining choices (4, 6, 8, 9). Nothing normative is drafted.

## DataChoice shape: a one-key map tested with has(), 2026-11-12

Asked, from Choice 8 of the draft mapping table, how a condition sees a DataChoice. The owner chose **a one-key map tested with has()** (recommendation followed; alternatives were the chosen name as a string only, and not readable).

- **Decided (direction):** a condition sees a choice as a map with exactly one entry, named after the chosen alternative, and tests which alternative is present with CEL's `has()` (for example `has(pos.latlon)`), then reads that alternative's fields. The type environment from the schema gives each alternative its own type. Reading a field of an alternative that is not chosen is an evaluation error and counts as no observation, under the decided rule.
- **Note:** this is the one mapping the standard invents; it is not in CEL or SWE Common. The standard must state it, and a test needs a conforming example.
- **Not decided (still open):** how the chosen alternative is read from the data (the schema's `choiceValue` category names it; mapping from that to the map's key is not worked out); the remaining choices (4, 6, 9). Nothing normative is drafted.

## Geometry: readable as numbers, limits stated, 2026-11-12

Asked, from Choice 9 of the draft mapping table, what the first version says about geometry. The owner chose **readable as numbers, state the limits** (recommendation followed; alternatives were requiring a matching reference system, and not readable until the function set exists).

- **Decided (direction):** a geometry is readable as a map holding its GeoJSON content (type and coordinates) and its reference system. The standard states that built-in CEL cannot test spatial relations, so a condition on a geometry can only compare coordinate numbers, and that numbers in different reference systems are not comparable (not enforceable in CEL; a Note). Spatial tests are left to the planned function-set extension.
- **Risk noted:** a condition may compare coordinates in the wrong reference system with no warning; nothing in the first version checks it.
- **Not decided (still open):** whether the reference system is declared and checked later (the "require a matching reference system" option, which needs a comparison rule like the unit one); the remaining choices (4 and 6). Nothing normative is drafted.

## Categories: plain text, no ordering, 2026-11-12

Asked, from Choices 4 and 6 of the draft mapping table (taken together; both concern category values), what a condition sees for a Category and a CategoryRange. The owner chose **plain text, no ordering** (recommendation followed; alternatives were plain text with a start-time check of codes, and not readable).

- **Decided (direction):** a Category is a CEL string and a CategoryRange is a pair of strings. CEL does not check that a code belongs to the schema's list or that a range makes sense. A Note says that conditions must not use ordering (`<`, `>`) on categories, because string order is not the codespace's order. Equality on a code works as expected.
- **Risk noted:** the start check does not catch a code written in a condition that is not in the codespace; a typo is a string comparison that is simply false.
- **Closes:** Choices 4 and 6 of the draft table. **All nine choices of the draft table are now decided.**
- **Not decided (still open):** nil values inside composite components; the unit-reference comparison rule; whether a reference system is declared and checked later; how the executor learns the result schema; verifying every mapping against the pinned SWE Common 3.0 text (the table was drafted from the API repository's JSON schemas); then converting the table into requirement records (not begun). Nothing normative is drafted.

## First records written, 2026-11-12

Asked whether the Architect may write the first requirement records, and which. The owner chose **terms plus an empty core class** (recommendation followed; alternatives were terms only, and not yet).

- **Done (all `status: proposed`, nothing `accepted`; identifiers are proposals, none assigned):** `records/term/*.yaml`, 21 term records, one file each, with the wording the owner accepted for now (definition and notes, as recorded above). No `source` and no `mappings` were written, because the owner has named no bibliography key or ontology address for them. `records/req/core.yaml` (`/req/core`, the identifier already named in `ogcspec.gate.toml`) and `records/conf/core.yaml` (`/conf/core`), both empty.
- **Gate:** stage 1 run on the 23 records: no findings, exit 0. This is a weak check: with no requirements, most rules pass trivially. Stage 2 (the compiled document) was not run; Metanorma was not run.
- **Differences from the accepted wording, for the owner to confirm:** (1) the bracketed reminder "(Kinds not yet decided.)" in the accepted "state" Note 2 was left out (it was an Architect's reminder, not wording, and the kinds are now decided); (2) a term record can hold only one `note`, so records with more than one note join them as "NOTE 1 ... NOTE 2 ..." in a single `note`; how the document emitter writes such a note was not checked (known gap in the term record format: "one note only"); (3) the term id slugs (for example `/term/capability-specification`) are the Architect's proposal; (4) `subject` of the core class is the placeholder `TO BE DECIDED BY THE OWNER` (the gate requires a subject; none was decided).
- **Not changed:** the accepted wording of "transition" (still not reopened for timeouts), "state" (Note 2 now answerable), and the accepted notes that restate rules; these records copy the accepted text as it stands.
- **Not decided (still open):** the core class's subject and what it requires; the first real requirement records; naming of fields and identifier segments; whether `style` groups are switched on in the gate config.

## Subject of the core class: implementation of the standard, 2026-11-12

Asked what the core requirements class is about. ModSpec Req 22 (clause "every requirements class ... other than the core ... SHALL have a standardization target type which is a subtype of that of the core") means the core's subject must cover the three things later classes will be about: capability specifications (documents), capability bindings (documents), and executors (software; decision 4.1 gives them their own class). The owner chose **implementation of the standard** (recommendation followed; alternatives were "capability specification", which bends the rule, and "documents only", which reopens decision 4.1).

- **Decided (direction):** the core class is about an implementation of the standard, broadly: anything that claims conformance, whether a document (specification or binding) or software (an executor). Each later class narrows it. `records/req/core.yaml` now has `subject: Implementation of the standard` (the option's label, written as the owner's choice; it replaces the placeholder). Gate stage 1 over the 23 records: no findings.
- **Consequence:** the word "implementation" needs a definition, which is **not drafted** and is not among the 21 accepted terms. A reader may find "implementation" loose for a document; the standard's Notes should say so (not drafted). Requirements shared by all three kinds (using the pinned references; identity and version) are candidates for the core class, not yet decided.
- **Not decided (still open):** the definition of "implementation"; what the core requires; the subjects of the other classes (capability specification, capability binding, executor) and their exact wording; whether the executor class lists the core directly (the gate config says every other class must). Nothing normative is drafted.

## First requirements: the identity and version rule, 2026-11-12

Asked where the identity-and-version requirement lives. The owner chose **a shared documents class** (recommendation followed; alternatives were repeating it in each class later, and putting it in the core class). Then asked how to word it. The owner chose **two requirements** (recommendation followed; alternatives were one requirement, and adding a same-document rule).

- **Written (all `status: proposed`; every identifier is the Architect's proposal, none assigned):** `records/req/document.yaml` (`/req/document`, subject "Document", inherits `/req/core`); `/req/document/identity` ("A document SHALL state its identity as a URI."); `/req/document/version` ("A document SHALL state its version as a text value."); their abstract tests `/conf/document/identity` and `/conf/document/version`; and the conformance class `/conf/document`. Gate stage 1 over the 29 records: no findings.
- **Left out on purpose:** the same-document rule (same identity and version means same document). The standard cannot test it, so it is not a requirement; it can become a Note or part of a definition if the owner wants it.
- **Open questions the requirements do not decide (not settled by the Architect):** (1) what counts as "a URI": a test needs a pinned definition such as RFC 3986, which is **not** among the ten normative references; (2) whether an empty or blank version counts as "a text value", and any length or character limit; (3) where in the document the identity and version are stated: field names are undecided, so the test steps can only say "locate the statement"; (4) the term "document" is not defined, and the records do not yet say that a capability specification and a capability binding are kinds of document; (5) "state" (in the document itself, or derivable from where it was retrieved) is not defined; (6) whether the binding follows the same rule (the owner's earlier note assumed yes; the shared class applies it to both).
- **Weakness of the abstract tests:** their steps restate the requirements ("check that the identity is a URI") with no input and no pass or fail rule beyond questions 1 to 3; they cannot be repeated by a tester until those are answered. Per the Architect's drafting rules, the owner's answers change the requirement first and the steps second.

## RFC 3986 pinned as the eleventh normative reference, 2026-11-12

Asked what "a URI" means in the identity requirement. The owner chose **pin RFC 3986** (recommendation followed; alternatives were leaving "URI" undefined, and using the JSON Schema "uri" format).

| Item | Value |
|---|---|
| Reference | RFC 3986, *Uniform Resource Identifier (URI): Generic Syntax*, T. Berners-Lee, R. Fielding, L. Masinter, Internet Standard STD 66, January 2005 (obsoletes RFC 2396, 2732 and 1808; updates RFC 1738) |
| Source | `rfc-editor.org/rfc/rfc3986.txt` (header read 2026-11-12) and the IETF Datatracker record (title, number and standard level confirmed) |
| Not verified | whether later RFCs update RFC 3986 (the "updated by" list was not retrieved this session); how the pin is worded in the normative-references clause (not drafted) |

- **Decided (direction):** RFC 3986 is the **eleventh** normative reference. The identity requirement and its test are worded against it. The pin is recorded here only: it is not in `ogcspec.gate.toml` (the gate config's reference list is for external requirements classes, not for documents like this) and no normative-references clause exists yet.
- **Written:** `/req/document/identity` now reads "A document SHALL state its identity as a URI as defined by RFC 3986." and its abstract test step "Check that the identity is a URI as defined by RFC 3986." Gate stage 1 over the 29 records: no findings.
- **Effect:** the check is of syntax only, not that the address resolves; an unregistered `urn:autonomyml` identifier is still a syntactically valid URI, so it passes even before registration. This answers open question 1 of the identity and version rule.
- **Not decided (still open):** blank versions, where identity and version are stated, and the undefined terms "document" and "state" (questions 2 to 5 of that rule).

## Names of identity and version: `uniqueId` and `version`, 2026-11-12

Asked what the identity and version are called inside a document. The example documents use `capabilityId` for specifications (with the version at the end of the identifier, for example `urn:autonomyml:capability:uxs-aerial:TakeoffSurveyAndRTL:0.1.0`); bindings have no identity, only a `capabilityRef` to a specification and a `targetSystem`; all documents carry `autonomyMLVersion`, `kind` and (specifications) `expressionLanguage` and `profile`. SensorML 3.0's `DescribedObject` has `uniqueId` ("URI serving as the globally unique identifier of the feature (typically a URN)") and a local `id` (read from the API repository clone, not the pinned text), and no version field. The owner chose **`uniqueId` and `version`** (recommendation followed; alternatives were `id` and `version`, and keeping the example names).

- **Decided (direction):** in a document, the identity is named `uniqueId` and the version is named `version`, on both specifications and bindings. The bare word "capability" is not used in these names.
- **Where it goes:** the documents class (`/req/document`) stays neutral about encoding. A later requirements class for the JSON encoding would say that these two names carry the identity and version; that class does not exist and is **not drafted**, and no record was changed by this decision. The abstract tests stay weak (they say "locate the statement") until that class exists.
- **Consequences for the examples (not edited):** `capabilityId` becomes `uniqueId` with the version moved to `version`; the bindings gain `uniqueId` and `version`; the version no longer rides inside the identifier.
- **Risk noted:** `version` can be confused with the examples' `autonomyMLVersion` (the format's own version), which this decision leaves alone; whether it stays, and under what name, is undecided.
- **Not decided (still open):** the JSON encoding class (its scope, and the pin for JSON itself, which is not among the eleven normative references); the name of the binding's pointer to its specification (`capabilityRef` uses the bare word) and of its system (`targetSystem`); blank versions; the terms "document" and "state"; the field for the document's kind. Nothing normative is drafted.

## JSON encoding classes started, RFC 8259 pinned as the twelfth reference, 2026-11-12

Asked whether to start the JSON encoding classes (decision 4.7: abstract requirements, JSON encoding separate and split by document kind). The owner chose **both kinds, three requirements each, and pinning RFC 8259** (recommendation followed; alternatives were the specification only, and not yet).

| Item | Value |
|---|---|
| Reference | RFC 8259, *The JavaScript Object Notation (JSON) Data Interchange Format*, T. Bray (Ed.), IETF Standards Track, December 2017 (obsoletes RFC 7159) |
| Source | header of `rfc-editor.org/rfc/rfc8259.txt` read 2026-11-12 |
| Not verified | its Internet Standard number (STD 90 is the Architect's recollection, not seen in the header read); whether later RFCs update it; the wording of the pin in a normative-references clause (not drafted) |

- **Decided (direction):** RFC 8259 is the **twelfth** normative reference (the eleven earlier ones plus this one), recorded here only (not in `ogcspec.gate.toml`).
- **Written (all `status: proposed`; every identifier is the Architect's proposal, none assigned):** `records/req/specification-json.yaml` (`/req/specification-json`, subject "Capability specification encoded as JSON") and `records/req/binding-json.yaml` (`/req/binding-json`, subject "Capability binding encoded as JSON"), each inheriting `/req/core` and `/req/document`, each with three requirements and tests: `json-text` ("A capability specification SHALL be a JSON text, as defined by RFC 8259, whose top-level value is an object."), `identity` ("The identity of a capability specification SHALL be stated in the top-level member named `uniqueId`."), `version` ("The version of a capability specification SHALL be stated in the top-level member named `version`."); the binding class says the same for a capability binding. Their abstract tests and the conformance classes `/conf/specification-json` and `/conf/binding-json`. Gate stage 1 over the 45 records: no findings.
- **Note on inheritance:** the classes list `/req/core` directly because the gate config's `core_dependency = "direct"` requires it (M012); the dependency on `/req/document` is the shared identity and version rule.
- **Effect on earlier tests:** the identity and version tests of `/req/document` are still abstract; these JSON tests are concrete ("locate the top-level member named `uniqueId`"). The JSON tests check that the member is present; that its value is a URI is checked by `/req/document/identity`.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) **duplicate member names:** RFC 8259 leaves a JSON object with two members of the same name unpredictable; whether a document with two `uniqueId` members fails is not decided; (2) whether "stated in the member" means only that it is present, or that its value is the identity (the tests check presence only); (3) the **binding** has no requirement for its reference to a specification or its system yet, because those field names (`capabilityRef`, `targetSystem`) are undecided, so the binding class is limited to the three rules; (4) the **examples** do not conform (they use `capabilityId`; bindings have no `uniqueId` or `version`); they were not edited; (5) the relation between "document" and the two accepted terms is still not stated in the records, so whether the JSON classes' subjects are "kinds of document" rests on the owner's reading; (6) STD number and updates of RFC 8259; (7) the two JSON classes repeat each other nearly word for word; whether they should share a class (decision 4.7 says split by kind) is not reopened.

## Binding reference to its specification: `specification` with address, identity, version, 2026-11-12

Asked how a binding names the specification it applies to. The examples use `capabilityRef` (one address, the version inside it). The owner chose **`specification` with address, identity and version** (recommendation followed; alternatives were `specification` as one URI, and keeping `capabilityRef`).

- **Decided (direction):** a binding has a top-level member named `specification`, an object with three members: `href` (the URI the executor resolves to fetch the document), `uniqueId` (the identity expected) and `version` (the exact version expected). At start the executor fetches `href` and rejects the start (REJECTED) if the retrieved document's own `uniqueId` and `version` do not match. The bare word "capability" is dropped from the name.
- **Settles:** the reference carries an expected identity and version (left open under "Identity and version" and "Reference form"); a binding names one exact version, not a range (left open under "Binding contents"); the "meant to point at" mechanism (left open under "Reference form"). The address and the identity are separate, so a URN identity that cannot be fetched still works.
- **Not decided (still open):** how the executor treats an `href` that redirects or needs authentication; whether `uniqueId` and `version` in the reference must themselves follow the documents class rules (assumed yes, since they repeat a document's identity and version); the member for the system and for the name mappings; the requirement wording (not drafted: no record changed by this decision). The example bindings do not conform (`capabilityRef`) and were not edited.

## Binding members: `system`, `dataStreams`, `controlStreams`, 2026-11-12

Asked how a binding names its system and maps the specification's local names to real streams. The example bindings have `targetSystem`, `csapiBaseUrl`, and per-stream groups `dataStreamBindings` and `controlStreamBindings` holding paths, an `expectedRateHz`, a `commandSchema` and (for one stream) an `onHaltAction`. The owner chose **`system`, `dataStreams`, `controlStreams`** (recommendation followed; alternatives were keeping the examples' structure, and one `mappings` list).

- **Decided (direction):** a binding has these top-level members: `specification` (decided above), `system` (a URI for the system it is for), `dataStreams` (maps each local input name to the full URI of a real datastream) and `controlStreams` (maps each local command name to the full URI of a real control stream). Nothing else.
- **Dropped from the examples:** `csapiBaseUrl` (full URIs make it unnecessary), `expectedRateHz` (the specification's maximum age covers freshness), `commandSchema` (the control stream carries its own schema), `onHaltAction` (a halt is the API's cancel and clean-up is in the specification, as decided). `processBindings` (in the aerial examples) is also not part of this shape; its role was not decided here.
- **Not decided (still open):** whether the system `system` must resolve to an API System resource, or may be any URI (assumed a URI; not decided); whether local names are unique across inputs and commands (assumed an input and a command may not share a name; not decided); what `processBindings` in the aerial examples was for (not examined) and whether a binding needs it; where the binding says how a halt reaches the control stream (the API's cancel is assumed; the earlier open question under "Halt details" is narrowed, not closed); the requirement wording (not drafted: no record changed by this decision). The example bindings do not conform and were not edited.

## Binding rules: reference and system written, mappings wait, 2026-11-12

Asked whether to write the binding requirements now. The owner chose **reference and system now** (recommendation followed; alternatives were all four, and not yet).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** two new requirements in `/req/binding-json`, with abstract tests and listed in `/conf/binding-json`: `/req/binding-json/specification` ("A capability binding SHALL state the capability specification it applies to in the top-level member named `specification`, an object whose members `href`, `uniqueId` and `version` are each stated.") and `/req/binding-json/system` ("A capability binding SHALL state the system it is for, as a URI as defined by RFC 3986, in the top-level member named `system`."). Gate stage 1 over the 49 records: no findings.
- **Not written, on purpose:** the mapping requirements (`dataStreams`, `controlStreams`), which refer to the inputs and commands a specification declares; the specification class does not exist yet. Also not written: the executor's start check (compare the retrieved document's identity and version with `specification`); the executor class does not exist.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) the `specification` test checks that the three members are present, not that `href` resolves or that `uniqueId` and `version` follow the documents class rules (the latter would follow from `/req/document` only if the reference counts as "a document", which it does not: the reference repeats a document's identity and version, and no requirement says so); (2) the `href` value is not required to be a URI as defined by RFC 3986 by this requirement (the reference-form decision says it is a URI); (3) whether the `system` URI must name an API System resource (assumed only a URI); (4) the duplicate-member question from the JSON classes applies here too; (5) the example bindings do not conform.

## Declared data in a specification: one variable per datastream, 2026-11-12

Asked how a specification declares the data its conditions read and how a condition writes a read. The examples use `interface.inputs` and `interface.parameters` (per-run inputs and constants), a `blackboard`, and functions the standard does not include (`withinPolygon`, `distance2D`). The owner chose **one variable per datastream** (recommendation followed; alternatives were one name per value, and keeping the examples' interface).

- **Decided (direction):** the specification has a member `dataStreams` with one entry per local datastream name. Each entry gives the datastream's maximum age and, for each quantity field the specification reads, the field path and its unit (and, for an array, matrix or stream field, its maximum size). In a condition, the local name is a CEL variable holding the latest observation in the API's own shape: for example `battery.result.level < 20.0` for a value and `battery.resultTime` for its time. The binding's `dataStreams` maps each local name to a real datastream (one to one).
- **Consequences for the examples (not edited):** `interface.inputs` (per-run inputs, deferred out of version 1), the `blackboard` (no counterpart in the decisions), and the functions `withinPolygon` and `distance2D` (built-in CEL only) do not carry over. `interface.parameters` (named constants such as `arrivalRadius`) has no decided counterpart: whether a specification may declare named constants, or writes the number into each condition, is **not decided**.
- **Not decided (still open):** the names of the entries' members (for example the maximum age and the unit declarations); how commands are declared (the `controlStreams` side; the matching question for the specification); whether the field path is written as dotted names or another form in the declaration; the requirement wording (not drafted: no record changed by this decision); named constants; the name of the specification member. Nothing normative is drafted.

## Declared commands in a specification: a variable per control stream, 2026-11-12

Asked how a specification declares the commands it can send and how a condition reads a command's status. The owner chose **a variable per control stream** (recommendation followed; alternatives were one built-in `command` variable, and status from a datastream only).

- **Decided (direction):** the specification has a member `controlStreams` with one entry per local command name. A command state names one of them and sends a command on it. In a condition, the local name is a CEL variable holding the latest command sent on that stream in the API's own shape, so a transition reads, for example, `navigate.currentStatus.statusCode == 'COMPLETED'` (or `'FAILED'`, `'REJECTED'`). The binding's `controlStreams` maps each local command name to a real control stream (one to one). This mirrors the datastream decision.
- **Consequences / assumptions (not decided):** a state sends one command at a time on a stream (the variable shows only the latest command); before the first command is sent, the variable has no value, which counts as no observation under the decided rules (a transition condition is not met); the status values are the API's own and are not redefined here.
- **Source note:** the member names `currentStatus` and `statusCode` come from the Part 2 clone at commit `fb858be` (2026-09-21), not the pinned edition; re-read the pinned v1.0 before any wording.
- **Not decided (still open):** what a command's parameter values are and how they are written (constants in the document, or CEL expressions); the form of a command state; whether a command state may send more than one command; the names of members inside a `controlStreams` entry; the requirement wording (not drafted: no record changed by this decision). Nothing normative is drafted.

## Command parameter values: constants in the document, 2026-11-12

Asked how the parameter values of a command are written. The owner chose **constants in the document** (recommendation followed; alternatives were CEL expressions evaluated on entry, and both).

- **Decided (direction):** a command state gives its parameters as fixed values written in the specification, in the control stream's own SWE Common JSON form. The values are known before the run, so the start check can check them against the control stream's schema, units included. Nothing is computed at run time.
- **Risk noted:** a command cannot use a value that comes from a sensor or another state, and a different target each run needs a different specification (per-run inputs are deferred). Expressions are a possible later extension.
- **Consequence:** the start check gains one more rejection: a constant that does not fit the control stream's schema (type, unit, range) rejects the start (REJECTED). How the check reads that schema is the same question as the result-schema one (the control stream's schema resource is assumed; not worked out).
- **Not decided (still open):** the form of a command state and its member names; whether named constants (the examples' `parameters`) exist, now that a command's values are literals; the requirement wording (not drafted). Nothing normative is drafted.

## Transitions: an ordered list, first match wins, 2026-11-12

Asked how a state declares its outgoing transitions and which wins when several conditions hold. The aerial example uses ASL-style `next` (unconditional), `catch` (on error), a `choice` state, `modeInvariants`, `startAt` and `timeoutSeconds`. The owner chose **an ordered list, first match wins** (recommendation followed; alternatives were an unordered set where overlap is an error, and keeping `next` and `catch`).

- **Decided (direction):** each state has a member `transitions`: a list of entries, each with a `condition` (CEL) and a `target` (the name of a state). When more than one condition holds, the first in the list is followed. A timeout is written separately, as a member `timeout` with a `duration` and a `target`. `next`, `catch` and the `choice` state are not used.
- **Closes:** the tie-break question "when several transition conditions hold at once" (left open under "Transitions: condition required").
- **Risk noted:** the order of the list now has meaning, so reordering a document changes its behavior; two transitions that overlap by accident are not detected. A timeout racing a transition condition (which first, when both hold at the same moment) is **not decided**.
- **Not decided (still open):** when transition conditions are evaluated (on each new observation, as invariants are, or on a schedule; open); the order between `transitions` and `timeout`; the names of the members `duration` and `target` (these are the Architect's reading of the owner's choice); the name of the invariants member; the requirement wording (not drafted). Nothing normative is drafted.

## When transitions are evaluated: on relevant news and once on entry, 2026-11-12

Asked when a state's transition conditions are evaluated. The owner chose **on relevant news, and once on entry** (recommendation followed; alternatives were a rate the state declares, and continuously at the executor's choice).

- **Decided (direction):** a transition's conditions are checked, in list order, once when the state is entered (after the entry actions and the invariant check, the decided order) and again whenever a new observation or command status arrives on a datastream or control stream that one of its conditions reads. "Relevant" means that the condition's text reads that stream's variable. A condition that reads only constants is checked only on entry. This is the same trigger as invariants.
- **Closes:** "when transition conditions are evaluated" (left open under "Transitions: an ordered list, first match wins"), and what "relevant" means for invariant checks (left open under "Invariant timing: each new observation"), by the same reading: a condition's text names the variables it reads.
- **Risk noted:** a state whose conditions read no stream and are not true on entry never moves on, except by a timeout or a halt; the executor must work out which variables each condition reads (assumed possible from the CEL text; not checked against CEL's own tooling).
- **Not decided (still open):** the order between `timeout` and `transitions` when both would fire at once; what happens when several news items arrive together (evaluated once per batch, or per item); the requirement wording (not drafted). Nothing normative is drafted.

## Invariants and actions: commands only, everything named, 2026-11-12

Asked how a state declares its invariants and its entry and exit actions. The owner chose **commands only, everything named** (recommendation followed; alternatives were an open set of actions, and no separate actions).

- **Decided (direction):** in version 1 an action is sending a command. An entry or exit action is a command on a declared control stream with constant parameters (the same form as a command state). A state may have `entryActions` and `exitActions` lists; each action has a `name`, its `controlStream` and `parameters`; an exit action also has a `timeLimit`. An action is finished when its command reports COMPLETED; a FAILED or REJECTED status, or passing the time limit, makes the clean-up fail. A state's `invariants` is a list of entries each with a `name`, a `condition` and a `response` (the target state). Names are unique across the specification, so a recorded cause can point at one.
- **Closes:** names unique (left open under "Recorded cause"); the field name of the exit-action limit (`timeLimit`); the invariant response's field name (`response`).
- **Consequence for accepted wording (not changed):** the accepted "action" definition says "operation that an executor performs as directed by a capability specification" and gives sending a command as an example; in version 1 that example is the only kind. A second kind of action is a possible later extension.
- **Not decided (still open):** whether a failed entry action fails the run or the state (not decided; the earlier open question stands); whether the exit-action `timeLimit` applies on an ordinary transition as well as on a halt (not decided; the earlier question stands); how an action's time limit is measured (from sending the command; assumed); what an action's command may be when the control stream is not mapped (the start check rejects a missing name: decided); the requirement wording (not drafted). Nothing normative is drafted.

## Failed actions: clean up, then end in fail, 2026-11-12

Asked what happens when an entry action fails, or an exit action fails during an ordinary transition (not a halt). The owner chose **clean up, then end in fail** (recommendation followed; alternatives were ending in fail at once, and following a declared `onFailure` transition).

- **Decided (direction):** an action failure (its command reports FAILED or REJECTED, or an exit action passes its time limit) ends the run in fail with the failed action as the recorded cause, after the executor runs the exit actions of the states that are active (innermost first, each within its time limit), the same clean-up as for a halt. This answers whether a failed entry action fails the run or the state (the run), and whether the exit-action `timeLimit` applies on an ordinary transition as well as on a halt (it applies to every exit action, wherever it runs).
- **Assumed, not decided:** if a clean-up action also fails or overruns, the run still ends in fail with the first failure as the cause; a state with no exit actions gets no clean-up; an action that fails during that clean-up is not retried.
- **Risk noted:** exit actions run after a command has already failed, which may be an unsafe situation; a state with no exit actions is left as it is.
- **Not decided (still open):** the wording of "ending in fail" through this path against the accepted "terminal state" ("state in which a run ends"): the run ends in fail without reaching a declared terminal state (the accepted wording, the "halted" Note and the fail terminal-state rule may need a Note; not decided); the order between `timeout` and `transitions`; batches of news arriving together; the requirement wording (not drafted). Nothing normative is drafted.

## Timeout against transitions: transitions first, 2026-11-12

Asked which is followed when a state's time limit passes at the same moment one of its transition conditions holds. The owner chose **transitions first** (recommendation followed; alternatives were timeout first, and the author declaring the order in the transitions list).

- **Decided (direction):** when the time limit passes, the executor first checks the state's transition conditions in list order and follows the first that holds; only if none holds does it follow the timeout. The timeout is a separate member, as decided.
- **Closes:** "the order between `timeout` and `transitions`" (left open under "Transitions: an ordered list, first match wins" and "When transitions are evaluated").
- **Risk noted:** a condition that holds only after the limit has passed does not count; "at the same moment" is not defined (an observation received before the limit expired is assumed to count; not decided).
- **Not decided (still open):** how received-before-expiry is judged (the executor's clock against the observation's time, or order of arrival); batches of news arriving together; the requirement wording (not drafted). Nothing normative is drafted.

## State members: named states with a `kind`, 2026-11-12

Asked what the states look like in a specification. The examples use `startAt`, `states`, `type` (values `csapiCommandAction`, `mode`, `behaviorTree`, `succeed`, `fail`) and `choice`. The owner chose **named states with a `kind`** (recommendation followed; alternatives were keeping the examples' names, and the owner naming them).

- **Decided (direction):** the specification has a top-level `initial` (the name of the first state) and `states` (an object of named states). Each state has a `kind`: `command` (with `controlStream` and `parameters`), `mode` (with its own `initial` and `states`, so nesting is a mode holding states), `behaviorTree` (members left to the optional class), or `terminal` (with `ending`, either `succeed` or `fail`). Any state except a terminal one may also have `transitions`, `timeout`, `invariants`, `entryActions` and `exitActions`. The examples' `succeed` and `fail` types become `terminal` states with an `ending`.
- **Closes:** the kind names (left open under "Kinds of state"), the initial-state field name (`initial`), the `states` member name, and the ending identifiers in documents for the two declared endings (`succeed` and `fail`; the identifier of the third ending, halted, is never written in a document, as decided).
- **Note:** these names were proposed by the Architect and chosen as offered; they are not the owner's own wording.
- **Not decided (still open):** whether a terminal state may sit inside a mode (assumed allowed); whether a mode may have its own `transitions` out of itself (assumed yes, taking effect when no child transition applies; not decided); behavior-tree state members (the optional class); the requirement wording (not drafted). Nothing normative is drafted.

## First specification requirements: the states, 2026-11-12

Asked which requirements to write first for capability specifications. The owner chose **the states first** (recommendation followed; alternatives were data and commands first, and everything in one pass). Wording was then offered in three cards (initial states; kinds and endings; transition rules), and the owner chose the recommended wording each time.

- **Written (all `status: proposed`; every identifier is the Architect's proposal, none assigned):** `records/req/specification.yaml` (`/req/specification`, subject "Capability specification", inheriting `/req/core` and `/req/document`) with seven requirements, their abstract tests, and `/conf/specification`: `initial` ("A capability specification that defines a state machine SHALL name exactly one of the states of that state machine as its initial state."), `mode-initial` ("A state of kind mode SHALL name exactly one of its child states as its initial state."), `kind` ("A state SHALL have exactly one kind, which is command, mode, behavior tree or terminal."), `ending` ("A state of kind terminal SHALL state its ending, which is succeed or fail."), `terminal-exit` ("A state of kind terminal SHALL NOT have a transition leaving it."), `condition` ("A transition SHALL state a condition."), `target` ("A transition SHALL state a target, which is a state of the same state machine."). Gate stage 1 over the 65 records: no findings.
- **Not written:** the JSON member names (`initial`, `states`, `kind`, `ending`, `transitions`, `condition`, `target`) in the JSON class; the existing `/req/specification-json` does not yet inherit `/req/specification`; every other batch (data, commands, invariants, actions, timeouts, names).
- **Open questions these requirements do not decide (not settled by the Architect):** (1) "mode" and "child state" are not defined terms; (2) the `initial` requirement says nothing about a state machine with no states; (3) whether a document that uses the kind "behavior tree" needs the optional class (an executor-side start check; not written); (4) whether a terminal state may have invariants, entry or exit actions (not decided); (5) whether a transition may target a state in another mode, or leave a mode (assumed yes; not decided); (6) the timeout, which also names a target, is not covered by the transition requirements; (7) state names unique within their parent (not decided); (8) the accepted "terminal state" and "state machine" definitions are restated by requirements 5 and 1 and stay unchanged; (9) the check that the condition is a valid CEL expression is not a document requirement (it is the executor's start check, not written).

## State names: unique across the whole specification, 2026-11-12

Asked how a transition's target names a state when states can be nested inside modes. The owner chose **unique across the whole specification** (recommendation followed; alternatives were unique within the parent with path targets, and unique within the parent with sibling-only targets).

- **Decided (direction):** every state name is unique in the whole specification, whatever mode it sits in. A transition's target, an invariant's response and a recorded cause can therefore point at one state by its name alone. This extends the name-uniqueness rule already decided for invariants, actions and commands, and settles the transition to a state in another mode (allowed, by name).
- **Cost:** authors cannot reuse a name such as "Hold" in two modes.
- **Closes:** "state names unique within their parent" (open question 7 under "First specification requirements: the states") and "whether a transition may target a state in another mode" (open question 5, answered yes).
- **Not decided (still open):** whether names of invariants, actions, commands and states share one namespace (so a state and an action may not have the same name) or are unique only within their own kind (assumed unique within their kind; not decided); the requirement wording (not drafted: no record changed by this decision). Nothing normative is drafted.

## JSON member rules for the states and the name-uniqueness rule, 2026-11-12

Asked for the wording of the JSON member rules for states, then for transitions, then for the state-name rule. The owner chose the recommended wording each time: **four requirements** for the states (the owner took the recommended option, which bundles the `states` and `initial` members in one requirement; the alternative, five atomic requirements, was offered and not chosen), **one requirement, order stated** for transitions, and **one requirement** for unique state names.

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification-json` (which now also inherits `/req/specification`): `/req/specification-json/states` ("A capability specification SHALL state its states in the top-level member named `states`, an object whose members are the states, each member named with the name of its state, and SHALL name its initial state in the top-level member named `initial`."), `kind` ("A state SHALL state its kind in its member named `kind`, whose value is one of `command`, `mode`, `behaviorTree` or `terminal`."), `mode-members` ("A state of kind mode SHALL state its child states in its member named `states` and name its initial state in its member named `initial`, in the same form as the top level."), `ending` ("A state of kind terminal SHALL state its ending in its member named `ending`, whose value is `succeed` or `fail`."), `transitions` ("A state that has transitions SHALL state them, in the order in which they are to be considered, in its member named `transitions`, an array of objects each having a member named `condition`, whose value is a string, and a member named `target`, whose value is a string that is the name of a state."). In `/req/specification`: `/req/specification/state-names` ("A capability specification SHALL NOT use the same name for two of its states, including states nested in modes."). Each has an abstract test, listed in `/conf/specification-json` or `/conf/specification`. Gate stage 1 over the 77 records: no findings.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) the `states` requirement bundles two rules (the `states` member and the `initial` member), which ModSpec disfavours; one failed test cannot say which broke; (2) `initial` is checked to name "the initial state", but no rule says it must name an existing state (the abstract `initial` rule says it names one of the states); (3) the `transitions` requirement states that array order is the order of consideration, but a test cannot check the author's intent, so no step covers it; (4) the `condition` string is checked only to be a string (that it is valid CEL is the start check, not written); (5) the characters a name may contain and case sensitivity; (6) whether a state and an action may share a name; (7) a state with no `transitions` is allowed; (8) the value `behaviorTree` (JSON) against "behavior tree" (abstract rule) is a spelling the Architect proposed; (9) the example documents do not conform (they use `startAt`, `type`, `next`, `catch`, `choice`, `succeed`, `fail`).

## Durations: SWE Common Quantity in seconds, 2026-11-12

Asked how a length of time is written in a specification (a datastream's maximum age, an exit action's `timeLimit`, a state's timeout `duration`). The owner chose **a SWE Common Quantity in seconds** (recommendation followed; alternatives were an ISO 8601 duration string, and a plain number of seconds).

- **Decided (direction):** a duration is a full-form SWE Common Quantity whose unit is seconds, for example `{"type": "Quantity", "uom": {"code": "s"}, "value": 5}`. This applies the earlier "full form only" decision. Only seconds (UCUM code `s`) are allowed; the Architect's proposal, taken as part of the choice: other time units and their conversion are not defined.
- **Not decided (still open):** whether `uom` may be given as a URI instead of a code (SWE Common allows either; assumed code only for durations); whether a value may be zero or negative (assumed positive only; not decided); the requirement wording (not drafted); the members that hold durations (`maxAge`, `timeLimit`, `duration` are the Architect's names). Nothing normative is drafted.

## What the CS API says about datastreams (the owner's question), 2026-11-12

Asked, in answer to the card on the shape of a `dataStreams` entry: "What does the CS API standard say about dataStreams?" Nothing was decided. The Architect read Part 2 (clause 8 "Datastreams & Observations", clause 20 JSON encoding, the JSON schemas `dataStream.json`, `baseStream.json`, `observationSchemaJson.json` and the example observation schemas) in the API repository clone.

- **Edition check:** the most recent commit touching `api/part2/standard` or `api/part2/openapi` is dated 2025-07-16, the pinned publication date (history was fetched from 2025-07-10 only). So the Part 2 text read matches the pin as far as the repository history shows; the published HTML was not read. This lifts the earlier caveat for Part 2 (not for SWE Common).
- **What a datastream is:** a `DataStream` is data produced by a single output of one `System`; all its observations share the same observed properties and result schema; it implements `sosa:ObservationCollection`, and an `Observation` implements `sosa:Observation`. It has a canonical URL and a nested endpoint under its system (`{api_root}/systems/{sysId}/datastreams`).
- **Its properties:** `name` (mandatory), `description`, `type` (`status` or `observation`), `validTime`, `phenomenonTime` and `resultTime` (the time spans of its observations; server generated), `observedProperties` (URIs), `resultType` (`measure`, `vector`, `record`, `coverage` or `complex`), `live` (is live data available), `formats` (the media types observations can be encoded in); and associations `system`, `observations`, `procedure`, `deployment`, `samplingFeatures`, `featuresOfInterest`. In JSON, `id`, `name` and `formats` are required; a datastream also carries `system@link` and an `outputName` (the system output feeding it).
- **The result schema:** each datastream has a schema resource per format at `{api_root}/datastreams/{id}/schema?obsFormat=...`. For `application/json` it holds `resultSchema` (a SWE Common component tree, "not necessarily a JSON schema" in general), an optional `parametersSchema`, or a `resultLink` with a `mediaType` when results are out of band. This is how an executor learns a datastream's result schema (the question left open under the type mapping).
- **What the CS API does not have:** no maximum age, no expected rate, no unit on the datastream itself (units live in the result schema's `uom`), nothing about field paths.
- **Two facts that matter to our decisions:** (1) a scalar result is a bare value (`"result": 23.5`) and the schema's top component has a `name`, so for a scalar the "field path" is empty; for a vector or record the path goes through named fields (`lat`, `position.lat`); (2) the API's own example scalar schema declares `NaN`, `-Infinity` and `+Infinity` as **nil values** (reasons `missing`, `BelowDetectionRange`, `AboveDetectionRange`), so under the decided rule ("NaN or a declared nil value is no observation") such infinities count as no observation exactly when the schema declares them; the "infinities stay readable" decision holds only where they are not declared nil.
- **Not decided:** the shape of a specification's `dataStreams` entry (the question remains open); whether the executor reads the `application/json` schema or another format's.

## A `dataStreams` entry: `maxAge` and a `fields` list, 2026-11-12

Asked, after the CS API findings above, what a `dataStreams` entry looks like. The owner chose **`maxAge` and a `fields` list** (recommendation followed; alternatives were separate `units` and `maxSizes` maps, and the owner naming the members).

- **Decided (direction):** each entry has `maxAge` (a duration: a SWE Common Quantity in seconds) and `fields`, a list of entries. Each field entry has a `path` (the nested field names joined by dots, for example `position.lat`; left out when the result is a single scalar value) and either `uom` (the unit expected, for a quantity; the start check compares it with the `uom` in the datastream's result schema) or `maxSize` (a whole number, for an array, matrix or stream). A field entry has exactly one of `uom` and `maxSize`.
- **Consequence:** the executor learns the result schema from the API's schema resource (`resultSchema` for `application/json`), as the findings above say; the standard does not duplicate it.
- **Not decided (still open):** whether `fields` may be empty or omitted (a datastream read only for freshness; assumed allowed); how two unit references are compared (the earlier open comparison rule); a field name that contains a dot (cannot be written); whether `maxAge` is required (assumed yes, as decided earlier: each datastream declares one); the requirement wording (not drafted). Nothing normative is drafted.

## Control streams in a specification: an array of local names, 2026-11-12

Asked what a `controlStreams` entry looks like. From the Part 2 clone (same edition check as above): a control stream has `system@link`, an `inputName`, `controlledProperties`, an `async` flag (whether commands are processed asynchronously: a synchronous stream returns a single COMPLETED, REJECTED or FAILED status; an asynchronous one can issue several status reports), and a command schema with a required `parametersSchema` (a SWE Common component tree), and optional `resultSchema` and `feasibilityResultSchema`. The owner chose **an array of local names** (recommendation followed; alternatives were an object mapping names to empty objects, and the owner naming it).

- **Decided (direction):** `controlStreams` is a list of text values, each a local command name that the specification uses, for example `["navigate", "hold"]`. The binding's `controlStreams` maps each of these names to a real control stream (one to one). Every name a state or an action uses must be in the list; the binding must map every name in the list.
- **Risk noted:** no place for per-stream information later without changing the member's shape (a breaking change to documents).
- **Not decided (still open):** whether a control stream name may be used by a state that does not send a command (not applicable); whether the executor checks a stream's `async` flag (the status variable works for both, but a synchronous stream returns only the final status; not decided); the requirement wording (not drafted). Nothing normative is drafted.

## Data and commands requirements written, 2026-11-12

Wording was offered in two cards (abstract rules; JSON member rules). The owner chose the recommended wording each time: **seven atomic requirements** and **six atomic requirements**.

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification`: `data-stream-declared`, `max-age`, `units`, `max-sizes`, `control-stream-declared`, `command-stream`, `declared-only` ("A capability specification SHALL declare each datastream that its conditions read, by a local name."; "A capability specification SHALL state a maximum age for each datastream that it declares."; "... SHALL state the unit expected for each quantity that its conditions read."; "... SHALL state a maximum size for each array, matrix or stream that its conditions read."; "... SHALL declare each control stream on which it sends a command, by a local name."; "A state or an action that sends a command SHALL name a control stream that the capability specification declares."; "A condition SHALL read only datastreams and control streams that the capability specification declares."). In `/req/specification-json`: `data-streams`, `max-age`, `fields`, `field-path`, `field-unit-or-size`, `control-streams` (the top-level `dataStreams` object, each entry's `maxAge` as a SWE Common Quantity in seconds, the `fields` array, each field's dotted `path` except for a single scalar value, exactly one of `uom` and `maxSize`, and the top-level `controlStreams` array of strings). Each has an abstract test, listed in the two conformance classes. Gate stage 1 over the 103 records: no findings.
- **Not written:** the binding mapping requirements (`dataStreams`, `controlStreams` in a binding; these can now be written against these declarations); the executor's start checks; invariants, actions, timeouts and command-state members; the name-uniqueness rules for invariants, actions and commands.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) "datastream", "control stream", "quantity", "array", "matrix", "stream", "local name" and "maximum age" are not defined terms; the SWE Common words rely on the pinned SWE Common 3.0; (2) "reads" for a condition is not defined (it means that the condition's text names the variable); (3) the `path` exception ("single scalar value") cannot be tested from the document alone, because whether the result is scalar depends on the datastream's schema, which the document does not contain; (4) a `maxSize` of zero, or a very large value; (5) the unit-reference comparison rule (how `uom` is compared with the schema's) is not written, since it belongs to the executor's start check; (6) the requirement that the `maxAge` Quantity's unit is seconds does not say how a unit is judged to be seconds (the UCUM code `s`; not stated in the wording); (7) the examples do not conform; (8) the specification-level and JSON-level requirements repeat each other closely; no mechanism links them beyond the class inheritance.

## Binding mapping requirements written, 2026-11-12

Asked for the structure and wording of the binding mapping rules. The owner chose **a new abstract class plus JSON rules** (recommendation followed; alternatives were JSON rules only, and the owner wording it).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** a new abstract class `/req/binding` (subject "Capability binding", inheriting `/req/core` and `/req/document`) with `data-streams` ("A capability binding SHALL map each datastream that its capability specification declares to a datastream of the system it is for.") and `control-streams` (the same for control streams), their tests and `/conf/binding`; and in `/req/binding-json` (which now also inherits `/req/binding`) `data-streams` ("A capability binding SHALL state the mapping of datastreams in the top-level member named `dataStreams`, an object whose members are named with the local names of the datastreams that the capability specification declares, each having as its value the URI, as defined by RFC 3986, of a datastream.") and `control-streams` (the same for `controlStreams`), with tests. Gate stage 1 over the 113 records: no findings.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) whether a binding may map a name that the specification does not declare (extra names; not decided; nothing forbids it); (2) whether a mapped URI must resolve, or must be the URI of a stream of the binding's own `system` (the abstract rule says "a datastream of the system it is for"; a test cannot check that without calling the API; the start check is not written); (3) the steps compare the binding with the specification, which a test of the binding alone cannot do (the test needs both documents); (4) "the URI of a datastream" is not defined (the API's canonical datastream URL, or any URL of a datastream); (5) the examples do not conform.

## One name list for states, invariants and actions, 2026-11-12

Asked whether a state, an invariant and an action can share a name. The owner chose **one list for all three** (recommendation followed; alternatives were separate lists per kind, and the owner explaining).

- **Decided (direction):** no two states, invariants or actions in a specification share a name, whatever their kind. A run's recorded cause is therefore just a name, with no kind. This closes "whether names of invariants, actions, commands and states share one namespace" (left open under "State names: unique across the whole specification").
- **Consequence for written records (not changed):** the proposed requirement `/req/specification/state-names` ("A capability specification SHALL NOT use the same name for two of its states, including states nested in modes.") covers states only. It no longer matches this decision; it needs rewording to cover invariants and actions (a change of wording that needs the owner's yes; offered in the next wording card).
- **Cost:** an author cannot call a state and an action by the same name (for example "Hold").
- **Not decided (still open):** the characters a name may contain, case sensitivity; what a "command" name is (a command is sent by a state or an action, so it has that state's or action's name; no separate name); the requirement wording. Nothing normative is drafted.

## Command, action, invariant and timeout rules written (abstract), 2026-11-12

Wording was offered in two cards (commands, actions and names; invariants and timeouts). The owner chose the recommended wording each time: **five requirements** and **four, with a permission**.

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification`: `command-parameters` ("A state of kind command SHALL state the parameters of its command as constant values."), `action-command` ("An entry action or an exit action SHALL send a command, with parameters stated as constant values."), `action-name`, `exit-time-limit` ("An exit action SHALL state a time limit, which is a duration."), `invariant-name`, `invariant-condition`, `invariant-response` ("An invariant SHALL state a response, which names a state of the same state machine as its target."), `timeout` ("A timeout SHALL state a duration and a target, which is a state of the same state machine."), each with an abstract test; the permission `/per/specification/timeout` ("A state other than a terminal state MAY state a timeout.", no test; not listed in a class, as the gate does not require it); and the existing `/req/specification/state-names` **reworded in place** to "A capability specification SHALL NOT use the same name for two of its states, invariants or actions." (same identifier; its test now collects the names of all three). Gate stage 1 over the 130 records: no findings.
- **Not written:** the JSON member rules for these (`controlStream`, `parameters`, `entryActions`, `exitActions`, `invariants`, `timeout`, `timeLimit`); the executor requirements; the start checks.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) "constant values", "duration" and "time limit" are not defined terms; (2) whether the parameters fit the control stream's schema is the executor's start check (not written); (3) a terminal state's invariants, entry actions and exit actions are not covered either way (the permission says a state "other than a terminal state" may have a timeout; the same limit for invariants and actions is not decided); (4) the permission is not listed in any class, so the document may not show it in a conformance clause (how the emitter handles a free-standing permission was not checked); (5) the response rule and the transition `target` rule repeat each other (the response is a transition in effect); (6) the examples do not conform.

## JSON member rules for commands, actions, invariants and timeouts written, 2026-11-13

Asked for the wording of the JSON member rules. The owner chose **fifteen atomic requirements** (recommendation followed; alternatives were seven grouped by construct, and the owner wording it).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification-json`: `command-stream`, `command-parameters`, `entry-actions`, `exit-actions`, `action-name`, `action-stream`, `action-parameters`, `time-limit`, `invariants`, `invariant-name`, `invariant-condition`, `invariant-response`, `timeout`, `timeout-duration`, `timeout-target`, each with an abstract test listed in `/conf/specification-json`. The specification's JSON class now has 29 requirements. Gate stage 1 over the 160 records: no findings. The `/req/binding-json` and the rest are unchanged.
- **Not written:** the executor class and its requirements (what an executor does with a specification: entering and leaving states, evaluating conditions, the clean-up, the recorded cause, the start checks); the document for terminal-state restrictions; the behavior-tree class.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) "a SWE Common component in full form that has a value" relies on the pinned SWE Common 3.0; no pinned JSON schema is named for it, so a tester would have to read the standard; (2) the action's member `name` next to the SWE Common component member `name` (used inside `parameters`) is not a clash by position but may confuse a reader; (3) the `condition` string is checked only to be a string (valid CEL is the executor's start check); (4) the requirement for `entryActions` and `exitActions` does not forbid them on a terminal state; (5) the specification JSON class has become long (29 requirements) and repeats the abstract class closely; whether to merge or keep split is not reopened; (6) the examples do not conform and were not edited.

## Executor class: how to divide it, 2026-11-13

Asked how to divide the executor's requirements into conformance classes. The owner chose **two classes: start and run** (recommendation followed; alternatives were one executor class of about 30 requirements, and three classes with halting and clean-up separate).

- **Decided (direction):** one class for what an executor does when a run is requested (resolve both references, confirm the binding supplies every declared name, type-check every condition, validate command constants, reject with REJECTED) and a second for what it does while running (enter and leave states, evaluate transitions, check invariants, timeouts, halting, clean-up, record the ending and cause). The run class depends on the start class, since running without the checks is not meaningful.
- **Not decided:** the class identifiers (the Architect's proposals only, none assigned); the exact requirements and their wording; the subject name (the proposal is "Executor"); whether "executor" and "implementation" need defined-term entries beyond the existing executor term. Nothing is written yet.

## Executor start class written, 2026-11-13

Asked for the wording of the start class. The owner chose **twelve atomic requirements** (recommendation followed; alternatives were five grouped requirements, and the owner wording them).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** class `/req/executor-start` (subject "Executor", inherits `/req/core`) with `accept-request`, `retrieve-specification`, `retrieve-binding`, `binding-version`, `binding-complete`, `type-check`, `unit-match`, `size-limit`, `constants-valid`, `rejected-status`, `one-run`, `no-early-entry`, each with an abstract test, and `/conf/executor-start`. Gate stage 1 over the 186 records: no findings.
- **Not written:** the run class; the recorded cause for a rejected request (not decided); the document-level rules.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) "retrieve" and "in progress" are not defined terms; (2) `unit-match` relies on the data stream's result schema carrying a unit for the field, which the pinned Part 2 and SWE Common text were not re-read to confirm; (3) `size-limit` relies on the result schema declaring an element count (a variable-size array declares none; the rule is silent on that case); (4) `type-check` assumes the executor builds the CEL environment from the result schemas, as decided, but no requirement states that environment; (5) the tests say "reject" but the rejection is observable only through `rejected-status`, so the abstract tests of 4 to 9 depend on it; (6) `no-early-entry` is partly redundant with the rejection rules and may overlap with the run class; (7) what a rejected request records or reports besides the status is not decided.

## Executor run class, first half written (moving between states), 2026-11-13

Asked for the wording of the first half of the run class. The owner chose **eleven atomic requirements** (recommendation followed; alternatives were six grouped requirements, and the owner wording them).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** class `/req/executor-run` (subject "Executor", inherits `/req/core` and `/req/executor-start`) with `begin-initial`, `enter-mode`, `command-on-entry`, `entry-actions`, `exit-actions`, `transition-order`, `first-match`, `evaluation`, `no-observation`, `transitions-first`, `timeout`, each with an abstract test, and `/conf/executor-run`. Gate stage 1 over the 210 records: no findings.
- **Not written (second half, next card):** invariant checking and responses, the ending of a run and its status code, the recorded cause, halting, the exit-action time limit, clean-up after an action failure, postconditions.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) whether a mode's own transitions apply while one of its child states is current: `first-match` says "its current state", which is the innermost state, so the specification does not yet say that a parent's transitions can fire; (2) the order in which several entry actions or several exit actions are performed (not decided); (3) "stale", "never-reported" and "nil" are not defined terms, and `no-observation` repeats the list in the decision on missing values instead of pointing at a defined term; (4) "performs" an action means sending its command, but sending is not yet defined to include waiting for the command's status; (5) the tests for `transition-order` and `evaluation` need a controllable test harness (a way to deliver observations and command statuses), which no requirement or clause describes; (6) `timeout` does not say what happens to a timeout when the executor re-enters the same state (the clock restarts on entry, implied by "since the state was entered", not tested).

## A mode's transitions while a child is current, 2026-11-13

Asked whether a mode's own transitions can fire while one of its child states is current. The owner chose **yes, parent first** (recommendation followed; alternatives were child first, and only the current state).

- **Decided (direction):** the executor checks the transitions of the enclosing modes, outermost first, and then those of the current state; the first condition met wins. An author can write a rule such as "battery low" once on the mode. This closes open question (1) of the previous section.
- **Reworded in place (owner's yes to "reword all three"; `status: proposed`, identifiers unchanged):** `/req/executor-run/first-match`, `/req/executor-run/evaluation` and `/req/executor-run/transitions-first` now speak of the transitions that apply to the current state, including those of enclosing modes, and the three abstract tests gained steps for a mode's transition. Gate stage 1 over the 210 records: no findings.
- **Not decided:** whether an enclosing mode's own timeout applies while a child is current (the present wording does not say, so today it does not); whether the same ordering applies to invariants (all enclosing invariants are already checked, per the earlier decision); a mode's transition that leaves the mode while a child's exit actions are pending (the transition-order rule covers the order of exits, not this case beyond it).
- **Cost recorded:** a parent's rule overrides a child's, which can surprise an author; the example documents do not yet show this.

## Executor run class, second half written (invariants, endings, halting, clean-up), 2026-11-13

Asked for the wording of the second half. The owner chose **thirteen atomic requirements** (recommendation followed; alternatives were five grouped requirements, and the owner wording them).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** added to `/req/executor-run`, each with an abstract test listed in `/conf/executor-run`: `invariants-checked`, `invariant-no-observation`, `invariant-response`, `end-on-terminal`, `end-succeed`, `end-fail`, `end-halted`, `cause`, `halt`, `exit-time-limit`, `second-halt`, `action-failure`, `no-resume`. The class now has 24 requirements. Gate stage 1 over the 236 records: no findings.
- **Open questions these requirements do not decide (not settled by the Architect):** (1) which cause a halt records (a halt has no declared name, since `halted` is never declared), and what the cause is for a run that ends by entering a terminal state (the terminal state's name is the natural choice but is not decided); (2) what happens when several invariants break at once; (3) what a failing postcondition does (postconditions are optional and have no run behavior; no requirement mentions them); (4) whether exit actions run when a terminal state is entered by a normal transition (the terminal-state restrictions on actions are not decided); (5) what "an action fails" means: command status FAILED or REJECTED, no status in time, or a command that cannot be sent; (6) what an exit action's time limit leaves behind: the command's own status after the executor stops waiting; (7) `exit-time-limit` and `halt` say nothing about an action failing during clean-up (the clean-up could loop); (8) the cause requirement says "a cause that is a name" without saying where the name is recorded or how it is read; (9) `no-resume` is testable only as the absence of behavior, so the abstract test has limited repeatability; (10) `end-succeed`, `end-fail` and `end-halted` repeat the status mapping from the decision on runs; (11) `invariant-no-observation` and `no-observation` repeat the list of no-observation values and should point at one defined term when the definitions are written.
- **Now written for the executor:** the start class (12) and the run class (24). Not written: the behavior-tree optional class, terminal-state restrictions, definitions of new terms (implementation, document, datastream, control stream, and others), the normative references clause, the examples, stage 2.

## Cause recorded for a halt, 2026-11-13

Asked what cause a halted run records. The owner chose **the name of the current state** (recommendation followed; alternatives were a name reserved by the standard, and no cause for a halt).

- **Decided (direction):** the cause of a halt is the name of the innermost state the run was in when the halt arrived. No reserved word is added. This closes open question (1) of the second-half section for halts only.
- **Cost recorded:** the cause says where the run was stopped, not why; the API's cancel carries no reason, so who or what canceled it is not recorded.
- **Not decided:** the cause for a run that ends by entering a terminal state, and for an action failure (next cards); where the cause is recorded and how it is read; the requirement wording. `/req/executor-run/cause` still says only "a cause that is a name" and is not changed.

## Cause recorded for a terminal state and for an action failure, 2026-11-13

Asked what cause a run records when it ends by entering a terminal state and when it ends because an action failed. The owner chose **the terminal state's name; the failing action's name** (recommendation followed; alternatives were also recording an invariant's name when it triggered the ending, and always the terminal state's name).

- **Decided (direction):** a run that enters a terminal state records that state's name as its cause; a run that ends because an action failed records the failing action's name; a halt records the innermost current state's name (previous section). Every cause is a name from the specification's one name list, so no reserved word exists.
- **Cost recorded:** when an invariant's response leads to a terminal state, the cause is the terminal state's name, so the invariant that fired is not recorded; authors can name the response state to say why.
- **Not decided:** where the cause is recorded and how it is read; the requirement wording (the written `/req/executor-run/cause` is not yet changed); what the cause is when a run ends in a terminal state while an action is also failing.

## Cause requirement reworded and split, 2026-11-13

Asked whether to replace the vague `cause` requirement. The owner chose **reword and split into three** (recommendation followed; alternatives were one reworded requirement, and leaving it as written).

- **Written (`status: proposed`, identifiers are proposals):** `/req/executor-run/cause` reworded in place to the terminal-state case; new `/req/executor-run/cause-action` and `/req/executor-run/cause-halt`; each with a rewritten or new abstract test; both listed in `/req/executor-run` and `/conf/executor-run`. The run class now has 26 requirements. Gate stage 1 over the 240 records: no findings.
- **Not decided:** where the cause is recorded and how it is read ("record" is as undefined as for the ending); a run that ends in a terminal state while an action is also failing; `/req/executor-run/halt` and `action-failure` do not mention the cause (the cause rules cover it).

## Several invariants broken at once, 2026-11-13

Asked which response the executor takes when several invariants are broken at the same moment. The owner chose **first, in the same order as transitions** (recommendation followed; alternatives were the current state's first then outward, and leaving it undefined).

- **Decided (direction):** the executor takes the response of the first broken invariant, checking enclosing modes from the outermost inward and then the current state, each list in the order stated. After the response transition the other invariants are checked again in the new state. This closes open question (2) of the second-half section.
- **Cost recorded:** an outer invariant always wins over an inner one; the author orders a state's own list to prioritise within it.
- **Not decided:** the requirement wording (next card); whether an invariant list is ordered in the abstract class (the JSON arrays are, the abstract rules do not say so).

## Invariant-order requirement written, 2026-11-13

Asked for wording of the invariant-order rule. The owner chose **add it as worded** (recommendation followed; alternatives were folding it into `invariant-response`, and the owner wording it).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/invariant-order` with an abstract test, listed in `/req/executor-run` and `/conf/executor-run`. The run class now has 27 requirements. Gate stage 1 over the 242 records: no findings.
- **Open:** the wording relies on the invariant list being ordered, which the abstract class does not say (the JSON arrays are ordered); "first broken invariant" after a response transition re-checks the other invariants only through `invariants-checked`.

## What counts as an action failing, 2026-11-13

Asked what counts as an action failing. The owner chose **REJECTED, FAILED or not sendable** (recommendation followed; alternatives were also counting a missing status within a time limit, and only FAILED).

- **Decided (direction):** an action fails when its command comes back with the status REJECTED or FAILED, or when the executor cannot send the command. This closes open question (5) of the second-half section.
- **Cost recorded:** a command that never answers is not a failure; only an exit action has a time limit, so an entry action can wait on an unresponsive stream until a transition, a timeout or a halt ends the wait.
- **Not decided:** whether a command CANCELED by someone else counts; whether an action must be COMPLETED before the run goes on (this affects what "wait" means in the entry rules); whether the same rule applies to the command of a command state (a state's command is not an action in the written rules); the requirement wording (`/req/executor-run/action-failure` still says only "when an action fails").

## Action-failure requirement reworded and command-failure added, 2026-11-13

Asked for wording of the failure rules. The owner chose **cover actions and state commands, as two requirements** (recommendation followed; alternatives were actions only, and one requirement for both).

- **Written (`status: proposed`, identifiers are proposals):** `/req/executor-run/action-failure` reworded in place ("…when the command of an entry action or an exit action is rejected, fails or cannot be sent…") with a rewritten test; new `/req/executor-run/command-failure` for the command of a state of kind command, with a test; both listed in the class and the conformance class. The run class now has 28 requirements. Gate stage 1 over the 244 records: no findings.
- **Open (not settled by the Architect):** (1) `cause-action` says "the failing action", but a failed state command is not an action, so the cause for a command failure is unwritten (the natural cause is the command state's name; to be asked); (2) a failure during clean-up (the exit actions run after a failure) is not covered, so clean-up could loop or the clean-up command's failure could change the ending; (3) whether a command CANCELED by someone else counts; (4) whether an action must be COMPLETED before the run goes on; (5) the "cannot be sent" case is hard to test repeatably.

## A failure during clean-up, 2026-11-13

Asked what happens when an exit action fails during clean-up (after a halt or a failure). The owner chose **carry on with the rest; ending unchanged** (recommendation followed; alternatives were stopping and ending as fail, and leaving it undefined).

- **Decided (direction):** a failing exit action during clean-up is skipped; the executor performs the remaining exit actions, then ends the run with the ending already decided (halted stays halted, fail stays fail). No second clean-up starts. This closes open question (2) of the previous section.
- **Cost recorded:** a failed clean-up is not shown by the status or the cause.
- **Not decided:** recording that a clean-up action failed; the requirement wording (nothing written yet: `halt`, `action-failure` and `command-failure` do not mention it); whether the same applies to an exit action that fails during an ordinary transition (not clean-up; today that is an action failure and ends the run with the ending fail).

## Clean-up failure and command-failure cause written, 2026-11-13

Asked for wording of both rules. The owner chose **add both as worded** (recommendation followed; alternatives were the clean-up rule only, and the owner wording them). The card's first requirement text contained a stray drafting line ("Hmm, precisely:") before the final wording; the final wording after it is what was written, and the slip is recorded here.

- **Written (`status: proposed`, identifiers are proposals):** `/req/executor-run/clean-up-failure` and `/req/executor-run/cause-command`, each with an abstract test, listed in the class and the conformance class. The run class now has 30 requirements. Gate stage 1 over the 248 records: no findings.
- **Open:** recording that a clean-up action failed (not decided); `cause-action` ("the failing action") and `cause-command` ("the state") are now separate and consistent; a command CANCELED by someone else; whether an action must be COMPLETED before the run goes on; postconditions (no requirement); the mode's own timeout; terminal-state restrictions.

## Postconditions are checked once, 2026-11-13

Asked whether a postcondition is checked once or must hold for some time. The owner chose **checked once, at that moment** (recommendation followed; alternatives were holding for a stated duration, and not supporting postconditions in version 1).

- **Decided (direction):** when a run enters a terminal state with the ending succeed, the executor evaluates each postcondition once, against the observations it holds at that moment, under the no-observation rule. If any is broken the run ends with the ending fail (FAILED) and the cause is that postcondition's name. This closes open question (3) of the second-half section and the "checked once" part of the 2026-11-12 postcondition decision.
- **Cost recorded:** a reading that is briefly right passes; a slow sensor that has not yet reported fails the run (an author can make the last state wait with a transition condition).
- **Not decided:** the member name (`postconditions` is the proposal); that postconditions share the one name list (would reword `state-names` again); whether postconditions are optional (assumed yes); what happens to the terminal state's exit actions; wording of every requirement (the specification's abstract and JSON rules and the executor rule; none written).

## Postcondition rules written, 2026-11-13

Asked for wording of the postcondition rules. The owner chose **write them as worded** (recommendation followed; alternatives were the executor rules only, and the owner wording them).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification`: `postcondition-name`, `postcondition-condition`, each with a test; the permission `/per/specification/postconditions` ("A capability specification MAY state postconditions.", no test, not listed in a class, like the timeout permission); `state-names` reworded in place to "…two of its states, invariants, actions or postconditions." with its test; in `/req/specification-json`: `postconditions`, `postcondition-name`, `postcondition-condition`; in `/req/executor-run`: `postcondition-check`, `postcondition-fail`, `cause-postcondition`, each with a test. The run class now has 34 requirements, the specification class 25, the specification JSON class 36. Gate stage 1 over the 265 records: no findings.
- **Open (not settled by the Architect):** (1) several broken postconditions: the cause is not decided (the first in stated order is the natural choice; the JSON array order is not stated in the abstract class); (2) what a terminal state's exit actions do (by the written rules a terminal state has none; the restriction is not written); (3) `postcondition-fail` and `end-succeed` can both apply to a run that reaches a succeed terminal state: the status mapping says COMPLETED, so `end-succeed` would need "unless a postcondition is broken", which is not written and the two requirements currently conflict for that case; (4) the permission's emitter handling is still unchecked; (5) the term "postcondition" Note says the requirements class for capability specifications states when it is evaluated, but the evaluation rule is in the run class.

## Conflict between succeed ending and postcondition removed, 2026-11-13

Asked whether to reword three run requirements. The owner chose **reword all three** (recommendation followed; alternatives were `end-succeed` only, and the owner wording them).

- **Reworded in place (`status: proposed`, identifiers unchanged, tests changed):** `end-succeed` now says "…with the ending succeed, and in which no postcondition is broken, as COMPLETED"; `end-fail` now says "…a run that ends with the ending fail as FAILED" (it previously missed runs that end as fail through an action or command failure or a broken postcondition, which enter no fail terminal state); `cause` now ends "…by entering that terminal state with no postcondition broken". Gate stage 1 over the 265 records: no findings. This closes open question (3) of the postcondition section.
- **Still open:** several broken postconditions (which name is the cause); whether a run that fails without entering a terminal state "ends" in the accepted sense of the terms "ending" and "terminal state".

## Several broken postconditions, 2026-11-13

Asked which postcondition is the cause when several are broken, and whether to add a requirement. The owner chose **the first in stated order; add a requirement** (recommendation followed; alternatives were recording all broken names, and leaving it undefined).

- **Decided and written (`status: proposed`, identifier is a proposal):** `/req/executor-run/postcondition-order` with an abstract test, listed in the class and conformance class. The run class now has 34 requirements. Gate stage 1 over the 267 records: no findings.
- **Cost recorded:** only one broken postcondition is recorded; the rule relies on the list being ordered, which the JSON array is and the abstract class does not say.
- **Still open:** whether the abstract classes say that lists of invariants, postconditions and transitions are ordered (several executor rules depend on it); a terminal state's exit actions; a command CANCELED by someone else; whether an action must be COMPLETED before the run goes on; whether an enclosing mode's timeout applies while a child is current.

## Order of transitions, invariants and postconditions written, 2026-11-13

Asked whether to add the missing order rules. The owner chose **three abstract rules and two JSON rewordings** (recommendation followed; alternatives were one abstract rule for all three, and JSON rewordings only).

- **Written (all `status: proposed`; identifiers are proposals):** in `/req/specification`: `transition-order`, `invariant-order` and `postcondition-order`, each with a test; in `/req/specification-json`: `invariants` and `postconditions` reworded in place to say "in the order in which they are to be considered" (as `transitions` already did), with a step added to each test. The specification class now has 28 requirements. Gate stage 1 over the 273 records: no findings.
- **Open:** the order of entry actions and of exit actions (not decided; no executor rule depends on it); "the order in which they are to be considered" is not a defined phrase; the identifiers `/req/specification/invariant-order` and `/req/executor-run/invariant-order` share a last segment in different classes (not a gate finding; may confuse a reader).

## Terminal state: no invariants, entry actions or exit actions, 2026-11-13

Asked what a terminal state may contain. The owner chose **no invariants, entry actions or exit actions** (recommendation followed; alternatives were allowing entry actions, and leaving it undefined).

- **Decided and written (`status: proposed`, identifiers are proposals):** in `/req/specification`: `terminal-invariants`, `terminal-entry-actions` and `terminal-exit-actions` ("A state of kind terminal SHALL NOT have …"), each with a test. The specification class now has 31 requirements. Gate stage 1 over the 279 records: no findings. A terminal state then states only its kind, name and ending; a final clean-up is the exit actions of the states left on the way in. This closes the "terminal-state restrictions" gap.
- **CONFLICT FOUND with accepted wording (not changed; owner decision needed):** the accepted term "terminal state" has Note 1 ("A terminal state has one ending: succeed, fail or halted") and Note 2 ("Halted is reached only by a halt that has completed the exit actions of the active states; a halt whose exit actions fail or overrun ends in fail"). The decisions since then say `halted` is never declared in a document (`/req/specification/ending` allows only succeed or fail), a halt that has an exit action fail or overrun is skipped and the ending stays halted (decision "A failure during clean-up", requirement `clean-up-failure`), and a halt is not a transition to a terminal state. Note 2 therefore contradicts `clean-up-failure` and Note 1 contradicts `/req/specification/ending`. The term record was not edited.
- **Not decided:** a timeout on a terminal state is not forbidden by a requirement (the permission only says a state other than a terminal state MAY state one).

## Four accepted term notes reworded, 2026-11-13

Asked whether to reword four accepted term notes that contradicted later decisions. The owner chose **reword the four notes** (recommendation followed; alternatives were changing the requirements instead, and leaving both).

- **Reworded in place (definitions unchanged; records stay `status: proposed`):** *terminal state* Note 1 (now "A terminal state has one ending: succeed or fail."), Note 2 (now "A halted run ends in no terminal state of the document."; Note 3 unchanged); *ending* Note (now "…and in halted when a halt stopped it."); *halt* Note (now "…the run ends in halted, whether or not those exit actions succeed."). Gate stage 1 over the 279 records: no findings. This resolves the conflict recorded in the previous section.
- **Cost recorded:** the accepted idea that a failed clean-up shows up as fail is reversed, as decided in "A failure during clean-up".
- **Not decided:** whether the earlier accepted-wording sections of this record (which still quote the old notes) need a pointer to this one (they are history and were not edited).

## Correction of requirement counts, 2026-11-13

Several sections above state the size of a class wrongly (counted by hand, not from the files). Counted from the class records on 2026-11-13: `/req/executor-start` 12, `/req/executor-run` 34, `/req/specification` 31, `/req/specification-json` 32. The earlier figures were corrected in place where they appeared as current counts; the 160, 210, 236 and later record totals come from the gate and stand.

## Behavior-tree optional class written (shape only), 2026-11-13

Asked how much of the optional behavior-tree class to write. The owner chose **shape only, six requirements** (recommendation followed; alternatives were a tiny core dialect now, and an empty class).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** class `/req/behavior-tree` (abstract; inherits core, document and specification) with `state-tree`, `root`, `node-type`, `node-children`, each with a test; the permission `/per/behavior-tree/node-type` ("A node MAY have a type that this standard does not define."; no test; not listed in a class); class `/req/behavior-tree-json` (inherits core, document, specification, specification-json and behavior-tree) with `tree`, `node-type`, `node-children`, each with a test; and `/conf/behavior-tree`, `/conf/behavior-tree-json`. Gate stage 1 over the 298 records: no findings.
- **Deviations from the card, by the Architect (flagged for the owner):** (1) the card's rule 5 ("A node of a type that the standard does not define SHALL NOT make the document nonconforming") was written as a **permission**, because it is a statement about conformance rather than a requirement on a subject; (2) the card's single JSON rule set (rule 6) was written as **three** atomic requirements (`tree`, `node-type`, `node-children`), following the class pattern. Neither changes the meaning; both can be reverted on request.
- **Not written:** node types, statuses, evaluation, endings and halting; an executor class for behavior trees (so an executor cannot yet claim the optional class); how the start check treats a document with a behavior-tree state on an executor that does not claim the class.
- **Open:** the core `/req/specification/kind` and `/req/specification-json/kind` rules still list behavior tree as a kind in the core class, although the kind is meant to be available only with this optional class (not reworded; this needs the owner's yes); the member names `tree`, `type`, `children` are proposals; `/req/behavior-tree/node-type` ("a type, which is a name") uses "name", which the one-name-list rule does not cover (node types are not unique); the behavior-tree state's own status and completion are undefined.

## API terms are defined by reference, 2026-11-13

Asked how to define the terms that come from the Connected Systems API (data stream, control stream, command). The owner chose **point at the API's definitions** (recommendation followed; alternatives were defining them in our own words, and starting with our own terms).

- **Decided (direction):** each API term becomes a term record whose definition says it is the API's term, with a source reference to the pinned OGC 23-001 or 23-002. The API stays the authority. Each reference needs a check against the pinned text before it is written (the earlier API reading came from the repository clone).
- **Terms counted as used but undefined (from the requirement statements):** control stream (10 uses), run request (10), mode (9), local name (9), cause (6), current state (5), duration (4), enclosing mode (4), data stream (3), plus "no observation" (stale, never-reported, NaN or nil) and "implementation"; "document", "retrieve", "in progress" and "reads" are also used. The standard's own terms are to be taken one at a time with two or three draft wordings each.
- **Not decided:** which API terms exactly (data stream, control stream, command, observation, command status are candidates; observation already has an accepted wording adopting SOSA/SSN); the form of a term's source field (the existing term records have none); the normative references clause.

## Three API terms written (command, control stream, data stream), 2026-11-13

Asked how the three API terms should read. The owner chose **copy the API wording, with a source line** (recommendation followed; alternatives were a pointer only, and the owner wording them).

- **Written (`status: proposed`; no identifier is assigned):** `/term/command` ("message that is sent to a system to trigger an actuation, and that contains the parameters of the actuation."), `/term/control-stream` ("collection of commands targeted at the same system, and sharing the same controlled properties."), `/term/data-stream` (alias "datastream"; "collection of observations acquired by the same system, and sharing the same observed properties."), each with `source: OGC-23-002` and `modified: true` (case and leading article only; the command definition's two sentences were joined). Gate stage 1 over the 301 records: no findings.
- **Source of the wording:** OGC 23-002 clause 4 as read from the repository clone (`opengeospatial/ogcapi-connected-systems`, commit `fb858be`), **not** the pinned published text. Part 1 (23-001) has no definition of these three terms; they are in Part 2. Each record carries a comment saying so.
- **Open:** the source key `OGC-23-002` is the Architect's proposal and matches no bibliography entry yet (the normative references clause is not written; the gate's form check passed, a stage 2 build may not); the API's definitions use "system" in the API's sense, while this standard has its own accepted *system* term; "command" here is the API's message, while the standard's requirements also say "the command of a state", which means the same message; the definitions must be checked against the published 23-002.
- **Not yet defined:** the standard's own terms (run request, mode, local name, cause, current state, enclosing mode, duration, no observation, implementation, document).

## "run request" defined, 2026-11-13

Asked which wording of "run request" to take forward. The owner chose **A: command that names the specification and binding** (recommendation followed; alternatives were a plain request, and no defined term).

- **Written (`status: proposed`):** `/term/run-request`: "command, sent to an executor, that asks it to start a run of a capability specification with a capability binding." NOTE: "The parameters of the command carry only references to the capability specification and the capability binding." Gate stage 1 over the 302 records: no findings. Not marked accepted; the owner has not accepted the wording as final (the usual acceptance step is separate).
- **Open:** the definition relies on the new, proposed *command* term; the Note repeats part of the start-class rule `accept-request`; "references" is not a defined term.

## "mode" defined, 2026-11-13

Asked how to define "mode", "child state" and "enclosing mode". The owner chose **A: one term, mode, with the others in a Note** (recommendation followed; alternatives were three separate terms, and no definition).

- **Written (`status: proposed`):** `/term/mode`: "state of kind mode, which contains child states." NOTE 1 "A mode has one initial child state, entered when the mode is entered." NOTE 2 "The modes that contain a state, directly or through other modes, are its enclosing modes." NOTE 3 "\"Mode\" here is a kind of state and is narrower than the \"control mode\" in the definition of state." Gate stage 1 over the 303 records: no findings.
- **Open:** "child state" and "enclosing mode" are not formal terms; Note 1 repeats a rule stated in the requirements; the accepted *state* definition still says "control mode", which Note 3 only explains; "current state" is not yet defined.

## "local name" defined, 2026-11-13

Asked which wording of "local name" to take forward. The owner chose **A: name given in the specification, supplied by the binding** (recommendation followed; alternatives were a short form, and no term).

- **Written (`status: proposed`):** `/term/local-name`: "name that a capability specification gives to a data stream or a control stream, and that a capability binding maps to a data stream or a control stream of a system." NOTE: "A local name is also the name by which a condition reads a data stream or a control stream." Gate stage 1 over the 304 records: no findings.
- **Open:** the Note states a fact the requirements also decide; the definition rests on the proposed terms *data stream* and *control stream*; whether a local name may be any string (characters, case) is not decided.

## "cause" defined, 2026-11-13

Asked which wording of "cause" to take forward. The owner chose **A: name recorded with the ending** (recommendation followed; alternatives were a short form, and no term).

- **Written (`status: proposed`):** `/term/cause`: "name, recorded with the ending of a run, of the item of the capability specification that ended the run or where it was when halted." NOTE: "The cause is the name of a terminal state, of a failing action, of a state whose command failed, of a broken postcondition, or, for a halt, of the innermost state the run was in." Gate stage 1 over the 305 records: no findings.
- **Open:** "item of the capability specification" is vague; the Note lists what the cause requirements already say and must be kept in step; a run rejected at start has no cause defined (the start class says nothing); the cause is not said to be a name in the one name list (the rule is on states, invariants, actions and postconditions).

## "no observation" defined, 2026-11-13

Asked which wording of "no observation" to take forward. The owner chose **A: define it, then reword the rules later** (recommendation followed; alternatives were a short form, and no term).

- **Written (`status: proposed`):** `/term/no-observation`: "absence of a usable value on a data stream or control stream, which is the case when the value has never been reported, is older than the maximum age, is not a number, or equals a nil value the schema declares." NOTE: "A condition that reads no observation is not met, and an invariant that reads no observation is broken." Gate stage 1 over the 306 records: no findings.
- **Not done (needs the owner's yes, a separate card):** rewording the requirements that repeat the list (`/req/executor-run/no-observation`, `/req/executor-run/invariant-no-observation`) to use the term; the data requirements in the specification class that mention it, if any.
- **Open:** "not a number" is narrower than the earlier decision's "NaN" (a decided NaN rule), though a number that is not a number is NaN by definition; a nil value inside a composite is undecided; "maximum age" is not a defined term; the term is a negative ("no observation"), which is unusual for a glossary entry; "observation" (accepted, SOSA/SSN) is a different thing.

## Two run rules reworded to use "no observation", 2026-11-13

Asked whether to reword the two rules that repeat the list. The owner chose **reword both** (recommendation followed; the alternative was leaving them).

- **Reworded in place (`status: proposed`, identifiers unchanged):** `/req/executor-run/no-observation` now reads "An executor SHALL treat a condition that reads no observation as not met."; `/req/executor-run/invariant-no-observation` now reads "An executor SHALL treat an invariant whose condition reads no observation as broken."; both tests reworded (the leading step names each case of no observation). Gate stage 1 over the 306 records: no findings.
- **Open:** `postcondition-fail`'s test still lists stale, never-reported, NaN and nil values by hand, and the postcondition rule does not use the term (the decided rule treats postconditions under the no-observation rule); a rule saying a postcondition that reads no observation is broken is not written.

## Postcondition reading no observation, 2026-11-13

Asked whether to add the missing rule. The owner chose **add one requirement, tidy the test** (recommendation followed; alternatives were rewording `postcondition-fail`, and leaving it).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/postcondition-no-observation` ("An executor SHALL treat a postcondition that reads no observation as broken.") with a test, listed in the class and conformance class; the last step of the `postcondition-fail` test (which listed the cases by hand) was removed. The run class now has 35 requirements. Gate stage 1 over the 308 records: no findings.
- **Open:** that a postcondition whose condition is false is "broken" is the ordinary meaning and not stated; the three "no observation" rules (condition, invariant, postcondition) are now a family of three near-identical rules.

## "current state" defined, 2026-11-13

Asked which wording of "current state" to take forward. The owner chose **A: the innermost state** (recommendation followed; alternatives were a longer form, and no term).

- **Written (`status: proposed`):** `/term/current-state`: "innermost state that a run is in at a given time." NOTE: "A run is also in each enclosing mode of its current state." Gate stage 1 over the 309 records: no findings.
- **Open:** "in a state" is not defined; the definition relies on there being one active child per mode (the no-parallel-states decision) which the glossary does not state; a run that has ended is in no state, and the term does not say what the current state is then.

## "duration" defined, 2026-11-13

Asked which wording of "duration" to take forward. The owner chose **A: length of time, in seconds** (recommendation followed; alternatives were no unit, and no term).

- **Written (`status: proposed`):** `/term/duration`: "length of time, in seconds." NOTE: "The JSON encoding states a duration as a SWE Common Quantity whose unit is seconds." Gate stage 1 over the 310 records: no findings.
- **Consequence recorded:** seconds is now part of the abstract meaning, so an encoding that used another unit would not state a "duration" in this standard's sense.
- **Open:** the Note names an encoding in a glossary entry; the abstract rules do not say how an encoding states a duration beyond this Note; whether fractions of a second are allowed is not decided.

## "document" defined, 2026-11-13

Asked which wording of "document" to take forward. The owner chose **A: a specification or a binding, as written** (recommendation followed; alternatives were any text that states one, and no term).

- **Written (`status: proposed`):** `/term/document`: "capability specification or capability binding, as written for an executor to read." NOTE: "The requirements that apply to both state them for a document." Gate stage 1 over the 311 records: no findings.
- **Open:** "as written for an executor to read" is loose; the JSON classes' subjects ("capability specification encoded as JSON") use a different phrase for the same idea; the postcondition JSON rule says "capability specification document", which now reads as "capability specification capability specification" in effect; the Note states what the requirements already do.

## "implementation" defined, 2026-11-13

Asked which wording of "implementation" to take forward. The owner chose **A: a document or an executor under test** (recommendation followed; alternatives were a product that can be tested, and no term with a changed core subject).

- **Written (`status: proposed`):** `/term/implementation`: "document or executor for which conformance to this standard is claimed." NOTE: "The requirements classes name the kind of implementation they apply to as their subject." Gate stage 1 over the 312 records: no findings. This closes the "implementation is not yet defined" note on the core class.
- **Open:** a document is an unusual thing to call an implementation; the definition does not say who claims conformance; the core class's file comment still says the term is not yet defined (a stale comment; not edited).
- **Terms now defined beyond the first 21:** command, control stream, data stream, run request, mode, local name, cause, no observation, current state, duration, document, implementation (twelve). Still undefined and used: "reads", "retrieve", "in progress", "references", "child state" and "enclosing mode" (the last in a Note only).

## Master document created with the normative references, 2026-11-13

Asked whether to create the master document with only the references filled in. The owner chose **references only, rest stays placeholder** (recommendation followed; alternatives were also drafting scope and conformance prose, and doing it later).

- **Written (new, `document/doc.adoc`, from the skeleton of the ogcspec-metanorma skill):** the twelve pinned normative references as bibliography entries with keys `OGC-23-001`, `OGC-23-002`, `OGC-23-000`, `OGC-24-014`, `W3C-SCXML`, `W3C-PROV-O`, `W3C-SOSA-SSN`, `ISO-IEC-21838-2`, `CCO`, `CEL`, `RFC-3986`, `RFC-8259`, each with the pinned edition or date from the pins table (CEL v0.26.0 and its commit, CCO v2.2 and its tag commit, the SOSA/SSN and BFO notes). The terms clause now includes `terms.adoc` (the skeleton's "No terms." line was replaced). The title, abstract, preface, scope, conformance prose, document number, external identifier, dates, author and organization remain the skeleton's `OWNER:` placeholders; **no OGC identifier is assigned**. The key `OGC-23-002` now exists for the three term sources. The records were not changed. Nothing was compiled or sent.
- **Not checked:** the titles are the Architect's wording of the pinned documents and were not compared with the publishers' pages in this step; the RFC STD numbers and "updated by" lists remain unverified and are not given; whether the entries' wording matches OGC's reference style; the bibliography keys are proposals.
- **Not done:** the stage 2 build (needs the pinned Metanorma image by digest; `emit.py` output and the build were not run); the master document's prose.

## First stage 2 build, 2026-11-13

Asked whether to use the one local Metanorma image for a first build and record its digest. The owner chose **use it; record the digest in the decision record** (recommendation followed; alternatives were building without recording a pin, and not now).

- **Build pin (recorded here only, not in any config file):** `metanorma/metanorma@sha256:daa12cf09812b34c6a62e67f5f78325847d56da534d7b7a23a45885496d36ae6`, tag `latest`, created about 7 days before 2026-11-13 and pulled on an unknown earlier date. It records what was used, not a version the owner chose. Nothing was pulled; the build ran offline (`--network none`) in a copy under the session scratchpad, not in the repository.
- **Emitter refusal fixed first (owner's yes, "move the citation to the source field"):** the emitter refuses a definition that contains a closing bracket, which stopped the first attempt at the accepted *observation* and *system* wordings ("… in SOSA/SSN [W3C SOSA/SSN, 2017]."). The bracketed citation was moved into each term's `source` field (key `W3C-SOSA-SSN`, with the ontology term's address and label, as the API writes it); the rest of each definition and the Notes are unchanged. Gate stage 1 over the 312 records after the change: no findings. These two accepted wordings were therefore edited.
- **Result:** the emitter wrote the fragments, Metanorma compiled (exit 0), and the gate's stage 2 reported **50 findings, all rule X010 (Metanorma log messages)**, and **none from the structural stage 2 rules** (no X000 to X004 finding). By kind:
  - `MODSPEC_1` (5): `/conf/core` has no test and `/req/core` has no requirement (the core class is empty, as designed); the three free-standing permissions (`/per/specification/timeout`, `/per/specification/postconditions`, `/per/behavior-tree/node-type`) are reported as having "no corresponding Conformance test". **This answers the earlier open question about how a free-standing permission is handled: it compiles, and Metanorma flags it.**
  - `STANDOC_7` (32): "element `term` not allowed here; expected the element end-tag", one for each term entry; the skill says these are expected for emitted terms with a source and are to be accepted through a baseline.
  - `STANDOC_40` (10): "Could not retrieve … no access to online site", one per bibliography entry, because the build is offline.
  - `RELATON_4` (2): "CEL" and "Common Core Ontologies" "do not have a recognised prefix" (they are not OGC, ISO, W3C or IETF identifiers).
  - `OGC_14` (1): "Submitters is missing!" (a placeholder in the master document).
- **Not done:** no baseline file was written (accepting messages needs the owner's yes); the compiled XML and logs are in the scratchpad build folder only. The compiler also printed "Document Attributes: '' is not a legal document type … reverting" messages, which come from the skeleton's placeholders (not carried into the gate's findings).
- **Open:** whether to accept these messages through a baseline; whether the permissions should have tests or be left flagged; where the build pin should finally live; the build was not repeated to show it is stable.

## Stage 2 baseline written, 2026-11-13

Asked how to handle the 50 Metanorma messages. The owner chose **baseline only the expected ones** (recommendation followed; alternatives were baselining all 50, and no baseline yet).

- **Correction:** the previous section gave the counts of two message kinds wrongly; counted from the gate's output they are `STANDOC_7` 32 and `STANDOC_40` 10 (with `MODSPEC_1` 5, `RELATON_4` 2 and `OGC_14` 1, total 50). The previous section was corrected in place.
- **Written (new file, `document/baseline.json`, 44 entries):** the term-element syntax notes (32), the "could not retrieve" notes for the offline build (10) and the two "no recognised prefix" notes (CEL, Common Core Ontologies). **Not accepted:** `MODSPEC_1` for `/conf/core`, `/req/core`, `/per/specification/timeout`, `/per/specification/postconditions` and `/per/behavior-tree/node-type`, and `OGC_14` "Submitters is missing!".
- **Tested:** the stage 2 gate against this baseline reports exactly those six messages as unexpected and none missing; the stage 1 run with the baseline reports no findings (the baseline's X entries are ignored in stage 1).
- **Open:** the six remaining messages (the empty core class has nothing to test; whether the three permissions should get tests or be accepted; the submitters placeholder); the baseline stores the build's message identifiers, which can change if the XML line numbers shift (the term notes are keyed by line: `STANDOC_7:XML Line …`), so adding or removing a term or a note can invalidate it; the baseline is not yet used by any recorded command.

## Permissions: listing in a class was refused by the gate; messages accepted, 2026-11-13

Asked what to do about the three free-standing permissions. The owner chose **list them in their classes; accept the message** (recommendation followed; alternatives were leaving them free-standing and accepting the message, and writing a test for each).

- **Tried and reverted:** I added each permission to the `requirements` list of its class and ran the gate. Stage 1 reported `M003` for all three ("lists … which is not defined as a requirement", 08-131r7 Req 28): the gate accepts only requirements in a class's list, not permissions. The records were restored to the committed state (the permissions stay free-standing, as written). This is a finding about the toolchain's rule, not a defect in the records: **a permission cannot belong to a requirements class here**, so its place in the document remains at the end of the requirements, outside any class.
- **Done (the owner's approval of "accept the message" applied):** the three Metanorma `MODSPEC_1` "no corresponding Conformance test" messages for `/per/specification/timeout`, `/per/specification/postconditions` and `/per/behavior-tree/node-type` were added to `document/baseline.json` (now 47 entries). The stage 2 build was repeated: the gate against the baseline reports three unexpected messages (the empty core class twice, and "Submitters is missing"), none missing.
- **Open:** a permission that belongs to no class has no subject and no conformance clause; whether that is acceptable to OGC's review (not asked); whether the permissions should become requirements (a "SHALL" form) or recommendations; the 08-131r7 Req 28 text was not read in this step.

## First conforming example written, 2026-11-13

Asked how to bring the examples in line. The owner chose **a new conforming example beside the old ones** (recommendation followed; alternatives were rewriting all six in place, and not now).

- **Written (new, in `examples/conforming/`; the six existing example files and the examples README were not touched):** `waypoint-navigation.spec.json` (two data streams, two control streams, four states: a command state with an invariant, an exit action, two transitions and a timeout; a safe-hold command state; one succeed and one fail terminal state; one postcondition), `waypoint-navigation.ugv-alpha-01.binding.json`, and `README.md` listing the gaps found. The identifiers are `example.org` URIs, placeholders and not assigned.
- **Checked:** only by a hand-written structural script (members present, names unique across states, invariants, actions and postconditions, targets exist, terminal states have no extra members, binding keys match the specification and its version). **Not checked:** CEL type-checking, SWE Common validation against the pinned schemas, the JSON classes' tests as run by a tool (none exists).
- **Gaps the exercise showed (in the folder's README, not decided):** no run-time inputs (command parameters are constants, so the target is fixed in the document); no distance function; no sustained postcondition; a redundant hold command from the exit action plus the safe-hold state; stale readings in the safe-hold state; lost error names; arrival depends on both the command status and the postcondition.
- **Not done:** the harder two examples (guarded navigation, aerial) were not converted: they rely on behavior trees with node types, a SensorML process, a blackboard and 3D reference systems, which the standard does not define; the examples README still describes the old files.

## Independent review deferred, 2026-11-13

Asked how to run the independent review of the 312 records. The owner chose **not now** (alternatives were a full review with the owner's own description, and a full review with a description built from the decided directions).

- **Effect:** the records have been checked only by the gate (stage 1 over 312 records, and the first stage 2 build) and by the Architect. No second reader has tried them as a tester or implementer would. No subagent was launched.
- **Open design questions still standing (the Architect's list, not ordered by importance):** whether an action must be COMPLETED before the run goes on; a command CANCELED by someone else; the order of several entry actions and of several exit actions; whether an enclosing mode's timeout applies while a child state is current; the core `kind` rules still list behavior tree; recording that a clean-up action failed; the undefined words "reads", "retrieve", "in progress" and "references"; nil values inside composites; the unit-reference comparison rule; the SWE Common mapping not checked against the pinned 24-014 text; the master document's prose; the ontology items (scope, name, IRIs, governance) and the `urn:autonomyml` registration (the owner's action).

## Entering a state does not wait for commands, 2026-11-13

Asked whether the run waits for a state's entry actions and its own command to finish before it checks transitions and timeouts. The owner chose **carry on at once; conditions decide** (recommendation followed; alternatives were waiting for every entry action, and also waiting for the state's own command).

- **Decided (direction):** on entering a state the executor sends its entry actions and its command and at once begins evaluating the state's transitions, invariants and timeout. Nothing waits for COMPLETED; a state that must wait writes a transition condition on the command status. Exit actions are the exception: the run waits for each, up to its time limit. This closes open question (4) of the clean-up-failure section.
- **Cost recorded:** an entry action still running when a transition fires is left running, not cancelled; an author must state any wait.
- **Not decided:** the requirement wording (none written); whether a command still running when its state is left is cancelled by the executor (not decided; the exit-action rules are silent); what a command's REJECTED or FAILED status does after the state has been left (the failure rules speak only of the command of an action or state that is current).

## No-wait requirement written, 2026-11-13

Asked for wording of the no-wait rule. The owner chose **add it as worded** (recommendation followed; alternatives were rewording `entry-actions` and `command-on-entry`, and leaving it in the record only).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/no-wait` ("An executor SHALL begin evaluating the transitions, invariants and timeout of a state when it enters the state, without waiting for the command of the state or of an entry action to complete.") with an abstract test, listed in the class and conformance class. The run class now has 36 requirements (counted from the class record). Gate stage 1 over the 314 records: no findings.
- **Open:** a command still running when its state is left (cancelled or left running: not decided); the overlap with `evaluation`; "perform" in `entry-actions` still means send.

## A running command is cancelled on leaving its state, 2026-11-13

Asked what the executor does with a state's own command or an entry-action command that is still running when the run leaves the state. The owner chose **cancel it, then do the exit actions** (recommendation followed; alternatives were leaving it running, and cancelling only on a halt or failure).

- **Decided (direction):** on leaving a state the executor first cancels the state's own command and any entry-action command that has not completed (the API cancel), then performs the exit actions. An author who wants a command to outlive its state sends it from an exit action. This closes the "running command" item of the no-wait section.
- **Cost recorded:** a cancel can itself fail or be ignored by the system, which is not covered; an exit-action command is not cancelled (it is waited for, up to its time limit).
- **Not decided:** the requirement wording (none written); a late FAILED or REJECTED status after the cancel; whether a halt cancels the commands of every state the run is in or only of the current state (the halt rule performs the exit actions of the states it is in, innermost first; the same order is the natural reading).

## Cancel-on-leave requirement written, 2026-11-13

Asked for wording of the cancel rule. The owner chose **add it as worded** (recommendation followed; alternatives were cancelling without fixing the order, and leaving it in the record only).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/cancel-on-leave` ("An executor SHALL, when it leaves a state, cancel the command of the state and the command of each entry action of the state that has not completed, before it performs the exit actions of the state.") with an abstract test, listed in the class and conformance class. The run class now has 37 requirements (counted from the class record). Gate stage 1 over the 316 records: no findings.
- **Open:** a failed or ignored cancel; "leaves a state" includes a halt and a failure, for which `halt` and `action-failure` say only "perform the exit actions"; whether a halt cancels the commands of every state the run is in (the natural reading is yes, innermost first); a state left because a postcondition is broken (the run is already in a terminal state, which has no commands).

## A mode's timeout applies while a child is current, 2026-11-13

Asked whether a mode's own timeout applies while one of its child states is current. The owner chose **yes, from entry to the mode** (recommendation followed; alternatives were only the current state's timeout, and forbidding a timeout on a mode).

- **Decided (direction):** a mode's timeout counts from the moment the mode is entered and keeps counting while any child is current. If it elapses and no transition of the mode, its children or enclosing modes is met, the executor takes the mode's timeout target. This closes the open question "whether an enclosing mode's timeout applies while a child is current".
- **Cost recorded:** the written `timeout` and `transitions-first` rules speak of the timeout of "a state" and of "its current state" and need rewording to cover enclosing modes.
- **Not decided:** which timeout wins when several have elapsed at the same moment (outermost first, as for transitions, is the natural reading); whether a transition between two children of the same mode restarts the mode's clock (by the decision it does not: the clock runs from entry to the mode); the requirement wording (nothing changed yet).

## Timeout rules reworded for enclosing modes, 2026-11-14

Asked whether to reword the two timeout rules. The owner chose **reword both** (recommendation followed; alternatives were rewording without an order for simultaneous timeouts, and the owner wording them).

- **Reworded in place (`status: proposed`, identifiers unchanged, tests rewritten):** `/req/executor-run/transitions-first` now reads "…before the timeouts of its current state and of the modes that enclose it."; `/req/executor-run/timeout` now reads "An executor SHALL take the target of the timeout of its current state or of a mode that encloses it, the outermost first, when the timeout's duration has elapsed since that state was entered and no transition has been taken." Each test gained steps for a mode's timeout (a clock that runs from entry to the mode, not from a change of child; two timeouts elapsing together). Gate stage 1 over the 316 records: no findings.
- **Architect's reading, not decided by the owner:** "the outermost first" for simultaneous timeouts (the card said so and the owner approved the wording).
- **Open:** the clock of a mode restarts only when the mode is re-entered (stated in the tests, not in a rule); a timeout on a state that has been left by a transition: the rule says the clock runs "since that state was entered", so re-entering a state restarts it (not tested).

## Order of entry and exit actions, 2026-11-14

Asked in what order the executor performs several entry actions or several exit actions. The owner chose **in the stated order, one after another** (recommendation followed; alternatives were order only for exit actions, and leaving all order undefined).

- **Decided (direction):** entry actions are sent in the order the document lists them; exit actions are performed in the listed order, each waited for (up to its time limit) before the next begins. Entry actions are only sent in order, not waited for (no-wait decision), so "in order" for them means the order sent, not the order they finish.
- **Cost recorded:** a slow exit action delays those after it, up to its limit.
- **Not decided:** the requirement wording (none written); whether a halt's or failure's clean-up uses the same order within one state (the natural reading is yes, innermost state first).

## Action-order rules written, 2026-11-14

Asked for wording of the action-order rules. The owner chose **write all six** (recommendation followed; alternatives were the executor and JSON rules only, and the owner wording them).

- **Written (all `status: proposed`; identifiers are the Architect's proposals, none assigned):** in `/req/specification`: `entry-action-order` and `exit-action-order`; in `/req/executor-run`: `entry-actions-order` ("An executor SHALL perform the entry actions of a state in the order stated.") and `exit-actions-order` ("…in the order stated, beginning each only when the previous one has completed or its time limit has elapsed."); each with a test; and `/req/specification-json/entry-actions` and `exit-actions` reworded in place to say "in the order in which they are to be performed" (a step added to each test). Counted from the class records: the specification class has 33 requirements and the run class 39. Gate stage 1 over the 324 records: no findings.
- **Open:** "completed" for an exit action means its command reached a final status, which is not defined; entry actions are only sent in order, not waited for, and the rule says "perform"; whether a halt's or failure's clean-up uses the same order within one state (the natural reading is yes); the identifiers `entry-actions` and `entry-actions-order` in the run class differ by one suffix.

## A command cancelled from outside the run, 2026-11-14

Asked what the run does when a state's or action's command ends with the status CANCELED because another party cancelled it on the control stream. The owner chose **treat it as a failure** (recommendation followed; alternatives were leaving it to the author's conditions, and treating it as a halt).

- **Decided (direction):** a command that comes back CANCELED when the executor did not cancel it counts as failing, like REJECTED or FAILED: the run performs the exit actions and ends with the ending fail, with the command's state or action as the cause. A cancel that the executor itself sent (on leaving a state, or on a halt) does not count. This closes the "CANCELED by someone else" item.
- **Cost recorded:** the failure rules widen by one case; an author's own condition on the status still works but the failure rule fires first for a command state's own command.
- **Not decided:** the requirement wording (nothing changed yet); how an executor tells its own cancel from another party's (it sent the cancel, so it knows; not stated); a command that is CANCELED after the executor's own cancel on leaving the state (covered by "did not cancel it").

## Failure rules reworded for an outside cancel, 2026-11-14

Asked whether to reword the two failure rules. The owner chose **reword both** (recommendation followed; alternatives were also rewording `clean-up-failure`, and the owner wording them).

- **Reworded in place (`status: proposed`, identifiers unchanged):** `/req/executor-run/action-failure` and `/req/executor-run/command-failure` now say "…is rejected, fails, is cancelled by a party other than the executor, or cannot be sent…"; each test gained steps (a command cancelled directly on its control stream is a failure; a cancel the executor sent itself on leaving the state is not). Gate stage 1 over the 324 records: no findings.
- **Open:** `clean-up-failure` was not changed, so an exit action cancelled from outside during clean-up is not covered; "a party other than the executor" is not a defined term; `cancel-on-leave` and these rules rely on the executor knowing which cancel it sent (not stated).

## Four kinds stay; executors reject unsupported kinds, 2026-11-14

Asked how to handle the core `kind` rules that still list behavior tree. The owner chose **keep four kinds; executors reject unsupported kinds** (recommendation followed; alternatives were removing behavior tree from the core kinds, and leaving it as written).

- **Decided (direction):** the core kind rules (`/req/specification/kind`, `/req/specification-json/kind`) are unchanged: a document may contain a state of kind behavior tree, and the optional class checks its shape. A class cannot loosen a rule it inherits, so the kind could not simply move into the optional class. The "available only where an executor claims the class" wording of 2026-11-12 is therefore met through the executor, not the document. This answers the earlier open question "whether the start check rejects a behavior-tree specification on an executor without the class".
- **Written (`status: proposed`, identifiers are the Architect's proposals):** `/req/executor-start/kinds-supported` ("An executor SHALL support states of kind command, mode and terminal.") and `/req/executor-start/unsupported-kind` ("An executor SHALL reject a run request when the capability specification has a state of a kind that the executor does not support."), each with an abstract test, listed in the class and conformance class. Counted from the class record, the start class now has 14 requirements. Gate stage 1 over the 328 records: no findings.
- **Cost recorded:** a document with a behavior-tree state is a conforming document that most executors will reject.
- **Open:** `kinds-supported` is a broad requirement (supporting a kind means all of the run class's behavior for it); `unsupported-kind` does not say the executor must say which kind; whether an executor class for behavior trees would add to or replace these rules (not decided; it would need a new class since a class cannot loosen these).

## "read" defined, 2026-11-14

Asked which wording of "reads" to take forward (and told that I would define "reads" and "in progress" and leave "retrieve" and "references" as ordinary English). The owner chose **A: names it in the expression** (recommendation followed; alternatives were "uses its value", and no term).

- **Written (`status: proposed`):** `/term/read`: "of a condition, to name in its expression the local name of a data stream or a control stream." NOTE: "A condition that names a local name reads that stream whether or not the value is used by the result of the condition." Gate stage 1 over the 329 records: no findings.
- **Architect's adaptation (flagged):** the card gave the sentence "a condition reads a data stream or a control stream if its expression names the local name of that stream"; the term record uses the glossary's definition style (a verb phrase, "of a condition, to name …") instead of a full sentence. The meaning is the same.
- **Open:** the rules use "reads" and "read" in running text, which the term "read" covers only if a reader accepts the verb forms; a condition's expression is not a defined term; how CEL writes a variable is not explained.

## "in progress" defined, 2026-11-14

Asked which wording of "in progress" to take forward. The owner chose **A: one term, for a run, with the halt in a Note** (recommendation followed; alternatives were two separate terms, and no term).

- **Written (`status: proposed`):** `/term/in-progress`: "of a run, started and not yet ended." NOTE: "A halt is in progress from the moment it is received until the run has ended." Gate stage 1 over the 330 records: no findings.
- **Open:** a run is "started" when the executor accepts the request (not stated); a rejected request is never in progress (not stated); the accepted *run* definition says a run goes "from its start until it reaches an ending" and the term relies on it.
- **Terms now defined beyond the first 21:** fourteen (command, control stream, data stream, run request, mode, local name, cause, no observation, current state, duration, document, implementation, read, in progress). "Retrieve" and "references" are left as ordinary English; "child state" and "enclosing mode" are only in a Note.

## Failed clean-up is recorded, 2026-11-14

Asked whether the run should record that an exit action failed during clean-up. The owner chose **yes: record the names of failed exit actions** (recommendation followed; alternatives were leaving it invisible, and making the ending fail).

- **Decided (direction):** besides the ending and the cause, a run records the names of the exit actions that failed during clean-up (a list, empty when none failed). The ending and the API status are unchanged. This closes the "recording that a clean-up action failed" item.
- **Cost recorded:** a second recorded item on every run; where and how the record is read is still undefined (as for the ending and the cause).
- **Not decided:** the requirement wording (none written yet); whether an exit action whose time limit elapsed counts as failed (an overrun); whether it covers exit actions that fail during an ordinary transition (there the action failure ends the run as fail, with that action as the cause).

## Clean-up-record requirement written, 2026-11-14

Asked for wording of the clean-up record rule and whether an overrun counts as failed. The owner chose **add it; an overrun counts as failed** (recommendation followed; alternatives were failures only, and the owner wording it).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/clean-up-record` ("An executor SHALL record, with the ending of a run, the name of each exit action that was rejected, failed, was cancelled by a party other than the executor, could not be sent, or reached its time limit, during clean-up.") with an abstract test, listed in the class and conformance class. Counted from the class record, the run class now has 40 requirements. Gate stage 1 over the 332 records: no findings.
- **Open:** where the record is kept and how it is read; the list of failure cases repeats the failure rules and must be kept in step; "during clean-up" is not defined (clean-up is used for the exit actions performed after a halt or a failure); an exit action that fails during an ordinary transition is not covered here (it ends the run as fail, with that action as the cause).

## Where the run record lives, 2026-11-14

Asked where the ending, the cause and the failed clean-up list should be kept. The owner chose **in the final status report's inline result** (recommendation followed; alternatives were the status message only, and leaving it undefined).

- **Decided (direction):** the ending is the final status code of the run's command (already decided: COMPLETED, FAILED or CANCELED); the cause and the failed clean-up list go in the inline result of the final status report, as members named `cause` (a string, the name) and `failedCleanUp` (an array of names). The executor's control stream declares a result schema with those two members. This answers "where the record is kept and how it is read".
- **Cost recorded:** a requirement on the executor's control stream is added; the names `cause` and `failedCleanUp` are the Architect's proposals; a client that ignores results sees only the status code; a REJECTED request (no run) has no cause or list (not required).
- **Not decided:** the requirement wording (none written yet); the form of the inline result for a REJECTED request; whether the result is also in earlier status reports (partial results); the existing "record" rules (`cause`, `cause-action`, `cause-halt`, `cause-command`, `cause-postcondition`, `postcondition-order`, `clean-up-record`) are unchanged and still say "record".

## Run-record requirements written, 2026-11-14

Asked for wording of the rules that fix where the run record is kept. The owner chose **write two new run requirements** (recommendation followed; alternatives were only the second rule, and rewording the seven existing rules).

- **Written (`status: proposed`; identifiers are the Architect's proposals, none assigned):** `/req/executor-run/result-schema` ("The result schema of the control stream on which an executor accepts run requests SHALL have a member named `cause`, a string, and a member named `failedCleanUp`, an array of strings.") and `/req/executor-run/record-in-result` ("An executor SHALL state the cause of a run and the names of its failed clean-up actions in the members `cause` and `failedCleanUp` of the inline result of the final status report of the run's command."), each with an abstract test, listed in the class and conformance class. Counted from the class record, the run class now has 42 requirements. Gate stage 1 over the 336 records: no findings.
- **Open:** the first rule's subject is the control stream's schema rather than the executor (a stretch of the class's subject, "Executor"); the seven existing rules still say "record" and now rely on `record-in-result` for the meaning; the result for a REJECTED request; partial results in earlier status reports; the "inline result" is the API's `CommandResult.inline`, whose encoding the API leaves to the control stream's result schema.

## A missing value inside a record: per field, 2026-11-14

Asked what counts as "no observation" when one field of a record result is missing (NaN or a declared nil value) and the others are fine. The owner chose **only what is read: per field** (recommendation followed; alternatives were the whole observation for any missing field, and leaving it undefined).

- **Decided (direction):** a condition that reads a field sees no observation only if that field has no usable value; other fields of the same result do not matter. A condition that reads a whole composite (a record, an array) sees no observation if any field inside it has no usable value. This closes the "nil values inside composites" item for the data rules.
- **Cost recorded:** a condition reading a whole composite fails more often; "any field inside it" has to be stated for arrays (any element).
- **Not decided:** the requirement wording (none written); a Note on the *no observation* term; whether a missing field inside a command parameter (constant) matters (parameters are constants and do not read streams).

## Composite no-observation rule written, 2026-11-14

Asked for wording of the per-field rule. The owner chose **one requirement plus a Note sentence** (recommendation followed; alternatives were the requirement only, and the owner wording it).

- **Written (`status: proposed`, identifier is the Architect's proposal):** `/req/executor-run/composite-no-observation` ("An executor SHALL treat a condition that reads a record or an array as reading no observation when any field of the record, or any element of the array, has no usable value.") with an abstract test, listed in the class and conformance class; and a second sentence added to the Note of `/term/no-observation`: "A condition that reads a field reads no observation only if that field has no usable value." Counted from the class record, the run class now has 43 requirements. Gate stage 1 over the 338 records: no findings.
- **Open:** "usable value" is not a defined term (it is used in the term's definition); "any field of a record" reads through nested records without saying so; the new rule covers conditions but not invariants or postconditions by name (the invariant and postcondition no-observation rules say "reads no observation", which the new rule defines for composites); the Note adds a rule-like sentence to a glossary entry.

## Unit references are compared exactly, 2026-11-14

Asked how two unit references should be compared. The owner chose **exact match of the same form** (recommendation followed; alternatives were equivalence by UCUM meaning, and leaving it to the executor).

- **Decided (direction):** two unit references are the same only if both are UCUM codes with identical text (case-sensitive) or both are URIs with identical text; a code never equals a URI. Anything else differs and the run is rejected. No conversion (already decided). This closes the "unit-reference comparison rule" item.
- **Cost recorded:** false rejections for equivalent spellings and for a code versus a URI naming the same unit; UCUM is not added to the pinned references.
- **Not decided:** the requirement wording (none changed yet); whether the check also applies to units inside a time, a vector or a range (not decided earlier either).

## unit-match reworded, 2026-11-14

Asked whether to reword the unit-match rule. The owner chose **reword unit-match, one sentence** (recommendation followed; alternatives were a separate requirement, and the owner wording it).

- **Reworded in place (`status: proposed`, identifier unchanged):** `/req/executor-start/unit-match` now ends "…, two units being the same only if both are UCUM codes with identical text or both are URIs with identical text."; its test gained steps (a different code, the same unit in another spelling, a code against a URI: rejected; an identical code or URI: not rejected). Gate stage 1 over the 338 records: no findings.
- **Open:** the sentence bundles the check with the definition of "the same"; "UCUM code" is used without UCUM being a normative reference; the abstract class (`/req/specification/units`) says only that the unit is stated and does not say how units compare.

## SWE Common mapping checked against the pinned text, 2026-11-14

The mapping table and the nine decisions on it were drafted from the API repository's JSON schemas. I re-read the pinned text (OGC 24-014, version 3.0.0, published 2025-07-16; the local published HTML in `~/ogc-references/swecommon/24-014.html`, requirement ids read from clauses 8 and 9). **No requirement wording was changed.** This section lists where the pinned text agrees with, differs from or adds to the earlier drafting. Nothing was decided here.

- **Agrees:** one JSON object member naming the chosen item for a DataChoice (`/req/json-encoding-rules/choice-object-valid`); a range is a two-value array (`range-value-valid`); a DataArray or Matrix is a JSON array (`array-values-valid`); a CategoryRange's code space is a well-ordered set (`category-range-codespace-order`), so "no ordering by string comparison" stands; a Category's value must be an entry of its code space when one is given (`category-value-valid`); a nil value must fit the component's type, a Boolean cannot have one and a Count's must be an integer (`nil-value-type-coherent`); Quantity's unit is mandatory.
- **Differs from the draft table:**
  1. **Special numbers.** The pinned strings are `NaN`, `-Infinity` and `+Infinity` (`special-numerical-values`), allowed for Quantity and for Time only when the time is not ISO 8601. There is no bare `"Infinity"`; the draft listed it. `+Infinity` is not the form CEL's own JSON conversion uses, so the executor must convert it.
  2. **DataStream is not a component.** It "does not derive from AbstractDataComponent" and cannot be a child of other components, so a result schema cannot be a DataStream. The decided row "DataArray, Matrix and DataStream readable as lists" needs the DataStream part dropped or restated (the stream is the wrapper, not a thing a condition reads).
  3. **Geometry.** The `srs` is an attribute of the component, not part of the value. The value is a GeoJSON geometry restricted to six types (no GeometryCollection), and its dimension must match the `srs`. The decided "map holding its GeoJSON content and its reference system" mixes two things; the reference system comes from the schema.
  4. **Optional record fields.** An optional field may be omitted or `null` (`record-object-valid`). Neither is in the decided list of no-observation cases (never reported, too old, NaN, declared nil).
  5. **Records and vectors may be arrays.** With `recordsAsArrays` / `vectorsAsArrays` the values are arrays in field order; the pinned sentence is self-contradictory about which setting gives which form, though the default is objects. The decided shape (a map read by field name) assumes objects.
  6. **Times.** A numeric time has a `referenceFrame` and optionally a `referenceTime`; the text says the frame "sometimes" implies the origin. The decided rule ("a number with a reference time") may exclude numbers whose origin the frame implies. An ISO 8601 time must carry the unit `http://www.opengis.net/def/uom/ISO-8601/0/Gregorian`.
  7. **Units may be given twice.** A unit reference may carry both a UCUM `code` and an `href`, and the pinned text requires both to name the same unit (`ucum-code-and-href-represent-same-unit`). The decided exact-match rule and the reworded `unit-match` do not say which form to compare when a field gives both.
  8. **Declared infinities are nil.** The pinned examples declare `-Infinity` and `Infinity` as nil values (below and above detection range). Under the decided rule such a value is no observation because it is declared nil; an undeclared infinity stays readable. This follows, but is worth a Note.
- **Not checked:** the encoded (text and binary) forms in clause 10; how an executor learns the result schema from the API (Part 2); time-zone and leap-second handling.
- **Open items this raises (each would be one card):** the unit form to compare when both are given (item 7); whether to drop DataStream from the mapping (2); how a missing or `null` optional field counts (4); whether numeric times with a frame-implied origin are timestamps (6); which record and vector forms an executor reads (5); how geometry and its `srs` are exposed (3).

## Units given as both a code and a URI: same if any form matches, 2026-11-14

Asked, from item 7 of the check against the pinned SWE Common text, how the start check compares units when a field states a UCUM code and a URI. The owner chose **same if any form matches** (recommendation followed; alternatives were every shared form must match, and code first then URI).

- **Decided (direction):** two units are the same if they share at least one identical UCUM code or at least one identical URI (text identical in each case); they differ, and the run is rejected, if no form is shared. A code is still never equal to a URI. This refines the exact-match decision of 2026-11-14 and rests on the pinned rule that a code and an href given together name the same unit.
- **Not decided:** the requirement wording (`/req/executor-start/unit-match` still says "both UCUM codes ... or both URIs", which does not cover a field with two forms; its test has no two-form step). Nothing changed in the records yet.
- **Still open from the check:** DataStream not a component; missing or `null` optional field; numeric time with a frame-implied origin; record and vector array forms; geometry and its `srs`.

## unit-match reworded again for both unit forms, 2026-11-14

Asked whether to reword the unit-match rule for the any-form decision. The owner chose **reword in one sentence** (recommendation followed; alternatives were leaving the wording, and the owner wording it).

- **Reworded in place (`status: proposed`, identifier unchanged):** `/req/executor-start/unit-match` now ends "…, two units being the same only if they share an identical UCUM code or an identical URI, a code never being the same as a URI."; its test gained two steps for a field giving both forms (a shared code, a shared URI, or both: not rejected; no shared form: rejected). Gate stage 1 run after the edit.
- **Open:** the specification's `uom` member is "a SWE Common unit reference" (`/req/specification-json/field-unit-or-size`), which allows a code, a URI or both, so a specification declaring both forms is covered. "UCUM code" is still not a normative reference.

## An omitted or null optional field is no observation, 2026-11-14

Asked, from item 4 of the check against the pinned SWE Common text, how an optional record field that is omitted or `null` counts. The owner chose **no observation** (recommendation followed; alternatives were an evaluation error with the same result, and rejecting at start unless the condition tests the field with `has()`).

- **Decided (direction):** a field that the schema marks optional and the value omits, or sets to `null`, is no observation. The per-field and whole-composite rules already decided apply to it. The "no observation" definition gains this case.
- **Not decided:** the wording (the term and its Note are unchanged); whether a missing field that is not optional is a data error or also no observation (SWE Common does not cover it; assumed: no observation, not decided).

## "no observation" reworded for an omitted or null optional field, 2026-11-24

Asked whether to put the 2026-11-14 decision into the records. The owner chose **reword the term and add test steps** (recommendation followed; alternatives were the term only, and the owner wording it).

- **Reworded in place (`status: proposed`, identifier unchanged):** `/term/no-observation` now ends "…, equals a nil value the schema declares, or is a field that the schema marks optional and the value omits or sets to null." The rules `/req/executor-run/no-observation` and `/req/executor-run/composite-no-observation` are unchanged; both follow from the definition.
- **Tests:** `/conf/executor-run/no-observation` gained the omitted and null optional-field cases in its supply step; `/conf/executor-run/composite-no-observation` gained a repeat step for an omitted and a null optional field. Steps drafted from the rule text only. Gate stage 1 run after the edit: 338 records, no findings (stage 2 rules not run).
- **Still not decided:** whether a missing field that is not optional is a data error or also no observation (assumed no observation; SWE Common does not cover it). The wording "or is a field that…" sits after "the value", so the sentence reads loosely; the owner approved it as proposed.
- **Still open from the check:** DataStream not a component; numeric time with a frame-implied origin; record and vector array forms; geometry and its `srs`.

## DataStream dropped from the SWE Common mapping, 2026-11-24

Asked, from item 2 of the check against the pinned SWE Common text, what the mapping says about DataStream. The owner chose **drop DataStream** (recommendation followed; alternatives were keeping it as "not readable", and keeping it as decided).

- **Decided (direction):** the mapping covers only what a data stream's result schema can contain. DataStream is not a component in the pinned text, so no condition reads one. Arrays and matrices stay readable as lists within the declared maximum size; out-of-band values stay not readable. This amends the 2026-11-12 Choice 7 decision, which named DataStream among the list types.
- **Changed:** the DataStream row in `docs/decisions/2026-11-12-draft-swe-common-to-cel-mapping.md` is struck through with the reason. No record changed: no requirement or test mentions DataStream.
- **Still open from the check:** numeric time with a frame-implied origin; record and vector array forms; geometry and its `srs`.

## Numeric time keeps the reference-time rule, 2026-11-24

Asked, from item 6 of the check against the pinned SWE Common text, whether a numeric time whose origin is only implied by its `referenceFrame` counts as a timestamp. The owner chose **keep: reference time required** (recommendation followed; alternatives were also accepting frames the standard lists, and reading numbers as plain numbers).

- **Decided (direction):** the 2026-11-12 Choice 5 rule stands. A numeric time is readable as a timestamp only if the schema gives a `referenceTime`; a numeric time with only a frame is rejected at start when a condition uses it as a time. The pinned text does not say which frames imply which origin, so no rule can rest on it. A later version may add a named list of frames.
- **Not decided:** the wording; no record about time exists yet. Also not covered: the unit a numeric time must carry, and the unit `http://www.opengis.net/def/uom/ISO-8601/0/Gregorian` the pinned text requires for an ISO 8601 time.
- **Still open from the check:** record and vector array forms; geometry and its `srs`.

## Records and vectors are read in object shape only, 2026-11-24

Asked, from item 5 of the check against the pinned SWE Common text, what an executor does with a record or vector sent as a bare list (`recordsAsArrays` / `vectorsAsArrays`). The owner chose **object shape only; reject the list shape** (recommendation followed; alternatives were reading both shapes, and asking the OGC authors first).

- **Decided (direction):** a condition reads records and vectors by field name. A result schema that sets either list-shape setting makes the start REJECTED. The standard does not rely on the pinned sentence about which setting gives which shape, which contradicts itself.
- **Not decided:** the wording; no record states it yet (it would sit among the start checks, `/req/executor-start`). Nothing is sent to OGC.
- **Still open from the check:** geometry and its `srs`.

## Geometry is read as the value only, 2026-11-24

Asked, from item 3 of the check against the pinned SWE Common text, what a condition sees of a geometry. The owner chose **value only; the `srs` stays in the schema** (recommendation followed; alternatives were exposing the `srs` as a second value, and rejecting geometry for now).

- **Decided (direction):** a condition reads the GeoJSON shape (`type`, `coordinates`) only. It cannot read the `srs`; the executor still does no reference-system check. Only the six GeoJSON geometry types the pinned text allows are readable (no GeometryCollection). This amends the 2026-11-12 Choice 9 decision, which put the `srs` beside the shape.
- **Changed:** the Geometry row in the draft mapping table. No record changed.
- **Not decided:** the wording; no record about geometry exists yet. Which six types, and whether a start check rejects a schema declaring another, are for the wording.
- **Closed:** this was the last open card from the check of the mapping against the pinned SWE Common text. All eight differences are now decided or noted; the "optional field" and "unit" ones are written in records, the rest are directions only.

## The executor reads application/json only; the list-shape direction is withdrawn, 2026-11-24

After the record-shape and numeric-time directions above, the owner declined to have two start rules written and said: "Seems like we are drifting from the CS API standard. Let's ensure we are matching that standard as much as possible." The Architect then read CS API Part 2 (local clone at master HEAD, `api/part2/standard/sections/clause_20` and `clause_21`; the clone-to-pin match is only known from commit dates) and found:

- **Plain `application/json` (clause 20):** the schema resource holds `resultSchema` with no `JSONEncoding` object; an observation has a `result` property "encoded according to the schema of the parent DataStream"; the API's own vector example sends the result as a named object (`{"lat": ..., "lon": ...}`). `recordsAsArrays` and `vectorsAsArrays` never appear.
- **`application/swe+json` (clause 21):** the schema key is `recordSchema` with an `encoding` set to a `JSONEncoding` object; an observation is one flat record following SWE Common's JSON encoding rules (24-014 clause 10.2), its time identified by a `definition` URI, with no `result` wrapper. The list-shape settings exist only here.
- **Not verified:** whether the API requires every datastream to offer `application/json`; the only requirement read (`/req/datastream/schema-op`) requires the schema operation and an `obsFormat` parameter.

The owner first chose to also allow swe+json, then, shown that the swe+json shape differs and would need mapping rules, chose **version 1: `application/json` only** (recommendation followed; alternatives were both formats with the executor rebuilding the plain shape, and both formats with the specification naming its format).

- **Decided (direction):** the executor learns a data stream's result schema from `{api_root}/datastreams/{id}/schema?obsFormat=application/json` and reads observations in that format only. This settles the question left open on 2026-11-12 (which format the executor reads). The condition shape (`battery.result.level`, `battery.resultTime`) stands.
- **Withdrawn:** the direction "records and vectors are read in object shape only; a list-shape setting makes the start REJECTED" (2026-11-24, above). In `application/json` a record or vector is always an object, so nothing needs rejecting. No record was written for it.
- **Consequence for time:** numeric time keeps the reference-time rule (Choice 5), but it now applies to `Time` components in a `resultSchema`; nothing yet says how the result's own time (`resultTime`, `phenomenonTime`) relates, those being ISO strings in the API's JSON.
- **Not decided:** the wording; a server that offers no `application/json` schema cannot be used (the standard says nothing more); swe+json, swe+text and swe+binary are possible later extensions. No record was written or changed.
- **Open:** whether to still write the numeric-time start rule, and whether the existing `/req/executor-start` rules should name the format (they say only "the result schemas of the bound data streams").

## Numeric time start rule written, 2026-11-24

The owner said "Start the numeric time rule now" after the `application/json` decision above. Written as `status: proposed`; identifier and wording are the Architect's proposals (the owner has not named them).

- **Written:** `/req/executor-start/time-origin` ("An executor SHALL reject a run request when a condition reads a Time field of a bound data stream whose unit is not http://www.opengis.net/def/uom/ISO-8601/0/Gregorian and whose result schema gives no referenceTime for it.") with test `/conf/executor-start/time-origin` (five steps: rejected without a reference time; not rejected with one; not rejected for an ISO 8601 unit; not rejected when the condition does not read the field). Added to `/req/executor-start` and `/conf/executor-start`. Gate stage 1: 340 records, no findings.
- **Reworded from the earlier proposal:** "numeric" is stated by the unit (anything but the ISO 8601 Gregorian unit, which the pinned SWE Common text requires of an ISO time), because a start check cannot see a value. The format is not named, so the rule applies to whatever result schema the executor reads.
- **Gaps, not decided:** whether TimeRange is covered (the 2026-11-12 table says "same caveat"; this rule names Time only); the rule rests on the Gregorian-unit statement from the pinned 24-014 text, read in the 2026-11-14 check and not re-read here; the term "Time field" and "referenceTime" are not defined terms; "reads" is.

## TimeRange joins the numeric time rule, 2026-11-24

The owner asked whether TimeRange is part of any upstream standard before deciding. Answer given: it is one of the four range types of SWE Common 3.0 (24-014, pinned); the published text of CS API Parts 1 and 2 and SensorML 3.0 never names it (0 mentions each; SensorML 3.0 has one mention in a diagram file, not opened); no CS API example schema read uses one. The pinned text says a TimeRange shares most properties with Time (checked: `referenceFrame`, `uom` with the ISO 8601 Gregorian unit; the JSON schema `TimeRange.json` has `referenceTime` and `uom`). The owner chose **extend the rule to TimeRange** (alternatives were leaving it out, and rejecting TimeRange).

- **Reworded in place (`status: proposed`):** `/req/executor-start/time-origin` now says "a Time or TimeRange field"; its test gained a repeat step for a TimeRange field. Gate stage 1: 340 records, no findings.
- **Noted:** this writes a rule for a type no upstream example exercises; it was chosen knowingly. The TimeRange `referenceTime` was read in the SWE Common JSON schema in the API clone (`swecommon/schemas/json/TimeRange.json`), not in the pinned HTML text.

## Format start rule written, 2026-11-24

Asked whether to write a rule for the `application/json` decision. The owner chose **write it as proposed** (alternatives were writing it without the rejection test, and not now).

- **Written (`status: proposed`; identifier and wording are the Architect's proposals):** `/req/executor-start/data-format` ("An executor SHALL obtain the result schema of each bound data stream from the schema resource of that data stream for the media type application/json, and SHALL read the observations of that data stream in the media type application/json.") with test `/conf/executor-start/data-format` (three steps). Added to `/req/executor-start` and `/conf/executor-start`. Gate stage 1: 342 records, no findings.
- **Gap:** the rejection step in the test (a data stream offering its schema only in another media type) is not in the sentence of the requirement; the owner approved the test as described, but the sentence does not say an executor rejects in that case. The rule does not say what happens if `application/json` is unavailable, and `rejected-status` (REJECTED) is the only existing start outcome. Wording to settle: either add "and SHALL reject a run request when it cannot" or drop the step.
- **Also:** a server offering no `application/json` schema cannot be used with version 1. Whether the API requires `application/json` of every datastream was not verified.

## What the CS API requires of formats; the format rule reworded, 2026-11-24

The owner asked what the API specifies before deciding on the rejection gap. Read in the pinned HTML (23-002, clause 2) and the clone's source (`clause_2_conformance.adoc`, `clause_8` `/req/datastream/schema-op`, `requirements_class_json.adoc`):

- **The API does not require `application/json`.** "There is no Core requirements class but an implementation target is expected to implement at least one of the CS resource types and one encoding." The encodings are JSON, SWE Common JSON, SWE Common Text and SWE Common Binary, each its own requirements class; a conforming server may offer only a SWE Common encoding. This answers the "not verified" item above: **the API does not require every datastream to offer `application/json`.**
- Each datastream lists its supported formats in the `formats` property, and `/req/datastream/schema-op` requires the schema resource to return a schema for the format named by `obsFormat`. The API allows extensions to add other formats.
- So `application/json` only is **narrower than the API**: a conforming server with no JSON encoding cannot be used with version 1.

The owner chose **keep JSON only; reject if absent, and say so** (alternatives were no rejection sentence, and reopening the format decision).

- **Reworded in place (`status: proposed`):** `/req/executor-start/data-format` now ends ", and SHALL reject a run request when a bound data stream does not offer the media type application/json."; the test's rejection step now has the executor check the `formats` of the data stream, and its purpose says the same. Gate stage 1: 342 records, no findings.
- **Not done:** the Note saying this is a version 1 limit narrower than the API. A requirement record has no `note` field (only terms have), so the limit is stated here only. A place for it in the document (an informative sentence in the clause, or in the term records) is open.

## Where the application/json limit is stated, 2026-11-24

Asked where to state that version 1 reads only `application/json`, narrower than the CS API. The owner chose **in the Scope clause, when you write it** (alternatives were a Note on the term 'data stream', and only in the rule).

- **Decided (direction):** the limit goes into the Scope clause when the owner writes it. Nothing is written into `document/doc.adoc`; its Scope and Conformance clauses stay `OWNER` placeholders.
- **Proposed one-sentence draft for the owner to reword:** "This standard reads the observations of a data stream only in the media type application/json; a server that offers a data stream only in a SWE Common encoding cannot be used with it."
- **Scope clause must also carry (carried forward):** nothing else yet; add items here as they arise.

## A missing required field is a data error that ends the run in fail, 2026-11-24

Asked what happens when a record result omits (or sets to null) a field the schema does not mark optional. The pinned SWE Common text lets only optional fields be omitted or null, so such a result breaks its schema; neither SWE Common nor the CS API says what a reader does. The owner chose **a data error that ends the run in fail** (alternatives were also no observation, which was the Architect's recommendation, and leaving it undefined).

- **Decided (direction):** a result that breaks its schema by leaving out a required field is a fault in a data stream the run depends on; the run ends with the ending fail and a cause naming the data stream. This differs from the optional-field case, which stays no observation.
- **Not decided (each a card):** what counts as a data error (only a missing required field, or any breach of the schema, and in which fields: only those a condition reads, or the whole result); the cause value (the local name of the data stream is assumed); what the run does on the way (clean-up with exit actions, as for a halt, assumed); whether the postconditions and invariants are checked; what a null value in a required field counts as; the effect on the existing rules `/req/executor-run/no-observation` and `/req/executor-run/composite-no-observation` and on the term "no observation". No record was written or changed.

## A data error is a missing required field in a field read, 2026-11-24

Asked what counts as a data error. The owner chose **(a) a missing required field, in fields a condition reads** (recommendation followed; alternatives were any schema breach in fields read, and validating every result against the whole schema).

- **Decided (direction):** a data error is a result that omits, or sets to null, a field that the schema does not mark optional, in a field that a condition reads. A wrong type, a value outside a constraint, or a breach in a field no condition reads is not covered in version 1.
- **Still open (each a card):** how the run ends and what the cause is; what a null in a required field counts as (assumed the same as omitted); the effect on the term and rules for no observation.

## A data error ends the run like an action failure, 2026-11-24

Asked how the run ends on a data error. The owner chose **same as an action failure** (recommendation followed; alternatives were ending in fail at once with no clean-up, and treating it as a broken invariant).

- **Decided (direction):** on a data error the executor performs the exit actions of the states it is in, innermost first, then ends the run with the ending fail; the cause is the local name of the data stream whose result broke its schema. Invariants and postconditions are not checked on the way.
- **Not decided:** the wording; a null in a required field counts as omitted (assumed); how this sits beside `/req/executor-run/composite-no-observation`, which says a condition reading a whole record reads no observation when any field "has no usable value" (a missing required field would also match that sentence).

## Data error records written, 2026-11-24

The owner chose **write all three as proposed** (alternatives were writing the two new rules only, and rewording first). All `status: proposed`; identifiers and sentences are the Architect's proposals.

- **Written:** `/req/executor-run/data-error` ("An executor SHALL, when a condition reads a field that the result schema of its data stream does not mark optional and the value omits that field or sets it to null, perform the exit actions of the states it is in, innermost first, and then end the run with the ending fail.") and `/req/executor-run/cause-data-error` ("…record the local name of the data stream as the cause of a run that ends under /req/executor-run/data-error."), each with a test; `/req/executor-run/composite-no-observation` reworded to end ", except that /req/executor-run/data-error applies when the field is one the result schema does not mark optional." with one added test step. Added to `/req/executor-run` and `/conf/executor-run`. Gate stage 1: 346 records, no findings.
- **Gaps, not decided:** the term `/term/cause` has a Note listing the kinds of cause (terminal state, failing action, state whose command failed, broken postcondition, halt); a data stream's local name is not in it, and the Note was not changed. "A condition" is read as any condition (transitions, invariants, postconditions, timeouts' conditions); not checked against how those rules say they read data. A null in a required field is treated as omitted (assumed). The start check does not know which fields are required at run time; it is run-time only. Postconditions and invariants are not checked on the way (direction decided; no sentence says so).

## Note on 'cause' extended, 2026-11-24

The owner chose **add it to the Note** (alternatives were leaving it, and rewording differently). `/term/cause` Note now lists "of a data stream whose result broke its schema" between the broken postcondition and the halt. Definition and rules unchanged; gate stage 1: 346 records, no findings. The Note still has no case for a broken invariant (its response state is a terminal fail state, so the cause is that state's name).

## Review finding: a halted run and the CANCELED status, 2026-11-24

An independent review (three readers; report in `_bmad-output/review-2026-11-24-records.md`, local only) found that the records conflict with the CS API for a halted run. Checked in the pinned 23-002 HTML: a cancel is "implemented by posting a new status report with status code CANCELED at the command status endpoint" (clause 14.5 note); CANCELED means "canceled by an authorized user", "must be used if the system supports user driven task cancellations", "The REJECTED state should be used instead if the command was canceled by the receiving system", and "This is a final state. No further status updates will be sent." A CommandResult is a separate resource: `{api_root}/commands/{cmdId}/result` is created with POST under Requirement 74 (class `/req/create-replace-delete`, optional), and a command has "a list of results generated during the execution of the command". The API does not say whether a result may be created after the command's status is final (silent).

The records had the executor report a halted run as CANCELED (`end-halted`) and write `cause` and `failedCleanUp` into the inline result of the final status report (`record-in-result`), which cannot work after a final CANCELED set by someone else. The owner chose **record in a CommandResult for every ending** (recommendation followed; alternatives were keeping the inline record for succeed and fail with none for halted, and having the executor post the CANCELED status itself).

- **Decided (direction):** for every run, whatever its ending, the executor creates a CommandResult on the run's command carrying `cause` and `failedCleanUp`; the CANCELED status of a halted run is set by the cancel, not by the executor.
- **Our reading, stated plainly:** creating a CommandResult after the command is final is a reading of an API silence.
- **Costs accepted:** the executor's API must implement the Create/Replace/Delete class (optional in the API); `end-halted`, `record-in-result` and `result-schema` change.
- **Not decided (open):** whether the CommandResult is created before or after the final status for succeed and fail; the status of `second-halt` (a second CANCELED after a final CANCELED cannot occur on a conforming server, so the rule is vacuous); which requirement states the executor's API classes; the wording.

## Halted run: records reworded, 2026-11-24

The owner chose **reword all three as proposed** (alternatives were rewording 1 and 2 only, and rewording first). All `status: proposed`; identifiers unchanged; sentences are the Architect's proposals.

- **`/req/executor-run/end-halted`:** "An executor SHALL NOT report a status code other than CANCELED for the command of a halted run." Its test now reads the status reports after the run ends and checks the status is CANCELED and no later report with another status code exists (the old test passed trivially).
- **`/req/executor-run/record-in-result`:** "An executor SHALL create, when a run ends, a CommandResult on the command of the run that states the cause of the run in a field `cause` and the names of its failed clean-up actions in a field `failedCleanUp`." Its test reads the CommandResult for a succeed, a halted and a failed run.
- **`/req/executor-run/result-schema`:** "…SHALL be a DataRecord with a field named `cause` of type Text and a field named `failedCleanUp` that is a DataArray whose elements are Text."
- **Gate:** stage 1 run after the edit: 346 records, no findings.
- **Still open:** `second-halt` unchanged (vacuous on a conforming server); whether the CommandResult is created before or after the final status for succeed and fail; no rule requires the executor's API to offer Create/Replace/Delete, an asynchronous run control stream, or cancel (review finding A2, to be asked); the term `/term/halt` and its Note unchanged; `clean-up-record` still says "record with the ending of a run" and was not changed.

## The executor's run control stream: four start requirements, 2026-11-24

From review finding A2. Checked in the pinned 23-002 HTML: `async` is a required ControlStream property ("whether commands are processed asynchronously"); for synchronous processing "a single status report is provided in the HTTP response" (COMPLETED, REJECTED or FAILED); `formats` is a required property (command encodings); CANCELED "must be used if the system supports user driven task cancellations". The owner chose **write all four in the start class** (alternatives were rules 1 to 3 only, and a new class).

- **Written (`status: proposed`; identifiers and wording are the Architect's proposals), each with a test, added to `/req/executor-start` and `/conf/executor-start`:** `run-stream-async` (the run control stream has `async` true), `run-stream-cancel` (it accepts a status report CANCELED), `run-stream-format` (its `formats` list application/json), `result-create` (the executor supports CREATE of CommandResult resources for its commands). Gate stage 1: 354 records, no findings.
- **Gaps:** the rules are about the executor's own API, not the start of a run, so the start class is a loose home (a new class was the alternative); the control-stream counterpart of `data-format` (which format the executor uses on control streams it commands, review finding A4) is not written; the tests do not say how a tester posts a CANCELED report as "an authorized user"; rule 4 relies on the optional Create/Replace/Delete class without naming it.

## Control streams: application/json and the component's value, 2026-11-24

From review finding A4. Checked in the pinned 23-002 HTML: a control stream's schema is fetched at `{api_root}/controlstreams/{id}/schema` with the `cmdFormat` parameter ("media type of the desired command format"); a control stream lists its command encodings in `formats`; the example command in the JSON encoding has `"parameters": {"pan": -10.0, "tilt": 23.0, "zoom": 0.4}`, a plain JSON value. The documents state a command's parameters as a SWE Common component in full form with a value. The owner chose **application/json; send the component's value** (recommendation followed; alternatives were changing the document form to plain JSON, and leaving it open).

- **Decided (direction):** the executor gets the parameters schema and result schema of a bound control stream from its schema resource for the media type application/json, sends commands in that media type, and rejects a run request when a bound control stream does not list application/json in `formats`; the `parameters` it sends is the value of the document's component. The Scope sentence about application/json must cover control streams too.
- **Not decided:** the wording, and the Scope sentence's extension.

## Control-stream format rules written, 2026-11-24

The owner chose **write both as proposed** (alternatives were splitting rule 1 into three, and rewording first). `status: proposed`; identifiers and sentences are the Architect's proposals.

- **Written:** `/req/executor-start/command-format` (the executor gets the parameters and result schemas of each bound control stream for application/json, sends its commands in application/json, and rejects a run request when the control stream does not list application/json in `formats`) and `/req/executor-start/parameters-value` (the executor sends, as a command's parameters, the value of the component the specification states), each with a test; added to `/req/executor-start` and `/conf/executor-start`. Gate stage 1: 358 records, no findings.
- **Scope sentence, extended draft for the owner to reword:** "This standard reads the observations of a data stream, and sends the commands of a control stream, only in the media type application/json; a server that offers a data stream or a control stream only in a SWE Common encoding cannot be used with it."
- **Gaps:** `command-format` bundles three obligations like `data-format` (the review suggested splitting both); `parameters-value` is our mapping, which the API does not define; `constants-valid` still says "the bound control stream's parameters schema" without naming the format (now sourced by `command-format`); the `result-schema` rule says the run control stream's result schema is a DataRecord, but nothing yet says the executor's own run stream must offer a `resultSchema` at all (it is optional in the API).

## A command in a condition is the API's Command: `currentStatus` is the status code, 2026-11-24

While preparing the CEL-environment rules (review finding B9) the Architect re-read the pinned 23-002 HTML and the clone: in a Command resource `currentStatus` is "current status code of the command", an enum value (the JSON example has `"currentStatus": "COMPLETED"`; the clone's `command.json` references `commandStatusCode.json`). A Command has no `statusCode` member; `statusCode` is a property of a CommandStatus report. The 2026-11-12 decision (and the line 1354 text above) wrote `navigate.currentStatus.statusCode == 'COMPLETED'`, which does not match what an API server returns. The owner chose **the Command as the API shows it** (recommendation followed; alternatives were keeping the decided shape as our own mapping, and using the latest CommandStatus report).

- **Decided (direction, correcting 2026-11-12):** a condition that reads a control stream sees the latest command in the shape the API returns; its status is tested as `navigate.currentStatus == 'COMPLETED'`. Other command properties (`issueTime`, `executionTime`, `parameters`, `sender`) are those of the API's Command.
- **Changed:** lines 56 and 57 of `examples/conforming/waypoint-navigation.spec.json` (`.currentStatus.statusCode` became `.currentStatus`); still a proposal, not validated. No record uses the old form.
- **Still open:** whether `currentStatus` is a CEL `string` (assumed); how a command that has no status yet reads (assumed no observation); which command is "the latest" on a shared control stream (review finding).

## CEL environment, batch 1 written, 2026-11-24

From review finding B9 (the SWE Common to CEL decisions had no records). The owner chose **write batch 1 as proposed** (alternatives were defining "latest" first, and rewording first). `status: proposed`; identifiers and sentences are the Architect's proposals; each has a test; added to `/req/executor-start` and `/conf/executor-start`. Gate stage 1: 366 records, no findings.

- **Written:** `condition-language` (a condition is evaluated as a CEL expression with only the functions the language defines; the CEL version pin, `v0.26.0`, is not in the sentence and stays in the normative references), `condition-bool` (a run request is rejected when a condition does not have the CEL type bool), `data-stream-variable` (a data stream's local name denotes the latest observation with `result`, `resultTime`, `phenomenonTime`), `control-stream-variable` (a control stream's local name denotes the latest command with the properties of the API's Command).
- **Open:** "latest" is undefined (resultTime for observations, issueTime or the executor's own command for a command on a shared stream, both assumptions); a data stream that has not reported is no observation, not a missing variable (no sentence says so); how `condition-language` relates to `type-check` (a function CEL does not define fails the type check); the test step for `condition-language` rests on the type-check rule for its rejection; the `statusCode` correction above.
- **Batch 2 (not started):** the CEL type of each SWE Common component in a condition, grouped into about six requirements (simple types, ranges, records and vectors, arrays and matrices, choices, geometry).

## "Latest" defined for the CEL variables, 2026-11-24

The API has a notion of latest only for observations (`resultTime=latest`: "only observations with the latest result time", optional advanced filtering class); for commands it has none and a control stream may be shared. The owner chose, for commands, **the last command this run sent on that stream** (recommendation followed; alternatives were the newest by `issueTime`, and leaving it open). Observations follow the API: the greatest `resultTime`.

- **Reworded in place (`status: proposed`):** `/req/executor-start/data-stream-variable` now says "the observation of that data stream with the greatest resultTime"; `/req/executor-start/control-stream-variable` now says "the last command that the run has sent on that control stream". Tests changed (observations published out of order; a foreign command on the same stream is not read). Gate stage 1: 366 records, no findings.
- **Noted, no change:** a control stream on which the run has sent no command reads as no observation under "never been reported" in `/term/no-observation`; the term was not changed. The earlier "one command at a time assumed" is superseded for the variable but a run that sends two commands on one stream in a row denotes only the last.

## CEL batch 2, scalar types written, 2026-11-24

Group 1 of about six for the CEL type of each SWE Common component in a condition. The owner chose **write it as proposed** (alternatives were one rule per type, and rewording first). `status: proposed`.

- **Written:** `/req/executor-start/scalar-types` ("In a condition, a value of a field of type Boolean SHALL have the CEL type bool; of type Count, int; of type Quantity, double; and of type Text or Category, string.") with a test; added to the start class and its conformance class. Gate stage 1: 368 records, no findings.
- **Gaps:** the rule bundles five types in one sentence; the test checks a compare with a literal of the right and of another CEL type, an observable effect of the start type check; the SWE Common mapping was drafted from the API repository's schemas and checked against the pinned text on 2026-11-14 (agreement for these types).
- **Next groups:** Time (how a number becomes a time; unit open), ranges, records and vectors, arrays and matrices, choices, geometry.

## Numeric time is in seconds only, 2026-11-24

Asked, for the CEL type of Time (CEL batch 2, group 2), how version 1 treats the unit of a numeric Time. The owner chose **seconds only; other units rejected at start** (recommendation followed; alternatives were any UCUM time unit converted, and not reading numeric time as a timestamp).

- **Decided (direction):** a numeric Time is the number of seconds after its `referenceTime` (UCUM `s`); a numeric Time with another unit that a condition reads makes the start REJECTED. This is narrower than SWE Common, which allows other time units; to be said plainly in the Scope draft.
- **Not decided:** the wording; whether a unit given as a URI for the second counts; whether the rule covers TimeRange (the time-origin rule does).

## CEL batch 2, Time written, 2026-11-24

The owner chose **write both as proposed** (alternatives were also accepting a second given as a URI, and rewording first). `status: proposed`; identifiers and sentences are the Architect's proposals; each has a test; added to the start class and its conformance class. Gate stage 1: 372 records, no findings.

- **Written:** `/req/executor-start/time-type` (a Time field has the CEL type timestamp: an ISO 8601 value is that date and time; a numeric value is the instant that many seconds after the field's referenceTime) and `/req/executor-start/time-unit` (a run request is rejected when a condition reads a Time or TimeRange field whose unit is neither the ISO 8601 Gregorian unit nor the UCUM code `s`).
- **Gaps:** a second given as a URI is rejected as written; "UCUM code" is not a normative reference; "ISO 8601 value" is not defined (the pinned text requires the Gregorian unit for an ISO time); TimeRange has no CEL type yet (ranges group); `time-origin` and `time-unit` overlap in cases, and the three time rules together are the full numeric-time rule.

## CEL batch 2, range types written, 2026-11-24

Group 3. The owner chose **write it as proposed** (alternatives were one rule per range type, and rewording first). `status: proposed`.

- **Written:** `/req/executor-start/range-types` ("In a condition, a value of a field of type CountRange, QuantityRange, TimeRange or CategoryRange SHALL be a list of two elements, the lower bound first, whose CEL type is int, double, timestamp or string respectively.") with a test; added to the start class and its conformance class. Gate stage 1: 374 records, no findings.
- **Gaps:** "lower bound first" relies on the pinned SWE Common text (a range value is a two-value array); a CategoryRange has no order, so "lower bound" is the first of its two code values (the standard says nothing about their order, per the 2026-11-12 decision, and no rule about string comparison was added); the rule bundles four types; a nil value or a missing bound inside a range falls under the existing composite rule.

## CEL batch 2, records and vectors written, 2026-11-24

Group 4. The pinned SWE Common 3.0 text says a vector coordinate "can thus only be of type Quantity, Count or Time", so the draft table's "a map of doubles" was wrong; a Vector is read like a record. In the application/json format records and vectors arrive as objects. The owner chose **write it as proposed** (alternatives were one rule each, and rewording first). `status: proposed`.

- **Written:** `/req/executor-start/record-types` ("In a condition, a value of a field of type DataRecord or Vector SHALL be a CEL map read by the name of each of its fields or coordinates, the value read having the CEL type of that field or coordinate.") with a test; added to the start class and its conformance class. Gate stage 1: 376 records, no findings.
- **Changed:** the Vector row of `docs/decisions/2026-11-12-draft-swe-common-to-cel-mapping.md` is corrected in place with a dated note.
- **Gaps:** the rule bundles two types; "read by the name" of a field is already enforced by the type check (a name the schema does not define fails it); a nested record is covered by the same sentence applied recursively, which the sentence does not say.

## CEL batch 2, arrays and matrices written, 2026-11-24

Group 5. The pinned SWE Common text (`/req/json-encoding-rules/array-values-valid`) encodes a DataArray and a Matrix as a JSON array of elements encoded by the element type's rules (its example includes a 2D array); it does not give a Matrix a row-major list-of-lists form. The owner chose **write it as proposed** (alternatives were one rule each, and rewording first). `status: proposed`.

- **Written:** `/req/executor-start/array-types` ("In a condition, a value of a field of type DataArray or Matrix SHALL be a CEL list whose elements have the CEL type of the element type of the field.") with a test; added to the start class and its conformance class. Gate stage 1: 378 records, no findings.
- **Changed:** the Matrix row of the draft mapping table is corrected in place with a dated note.
- **Still unwritten from the decisions:** the run-time rule (an array larger than its declared maximum size is no observation) and out-of-band results (a `result@link`, no inline result, are not readable); `size-limit` and `max-sizes` still say "or stream".

## CEL batch 2, choice and geometry written, 2026-11-24

Group 6, closing the CEL type groups. The owner chose **write both, with the choice exception** (alternatives were handling the conflict in `data-error`, and rewording first). `status: proposed`.

- **Written:** `/req/executor-start/choice-type` ("...a CEL map with one key, the name of the chosen item, whose value has the CEL type of that item; an item of a DataChoice is not a field that the result schema does not mark optional.") and `/req/executor-start/geometry-type` ("...a CEL map with the members type and coordinates of the GeoJSON geometry, and no member for the coordinate reference system."), each with a test; added to the start class and its conformance class. Gate stage 1: 382 records, no findings.
- **Why the exception:** the unchosen items of a DataChoice are omitted by design, and `/req/executor-run/data-error` would otherwise end a run that tests them with `has()` (review finding).
- **Gaps:** the exception sentence is a double negative the owner approved as proposed; it sits in a type rule instead of in `data-error`; the six allowed GeoJSON types are not listed in the rule (the pinned text restricts them); the geometry test's second step relies on the type check rejecting an unknown member; the has() test needs a DataChoice with `has()` available in the CEL environment.
- **CEL batch 2 is complete** apart from the unwritten run-time size and out-of-band rules.

## Size, out-of-band and result schema: three changes, 2026-11-24

The owner chose **write all three as proposed** (alternatives were items 1 and 2 only, and rewording first). `status: proposed`.

- **Reworded in place:** "or stream" removed from `/req/specification/max-sizes`, `/req/executor-start/size-limit` and their tests (a DataStream is not a component). `/term/no-observation` now ends "…or has more elements than the maximum size that the specification declares for it, or is held out of band."; the supply step of `/conf/executor-run/no-observation` gained both cases.
- **Written (review finding A7, not earlier decided):** `/req/executor-start/result-in-schema` ("An executor SHALL reject a run request when the schema resource of a bound data stream gives no resultSchema.") with a test; added to the start class and its conformance class.
- **Gate:** stage 1, 384 records, no findings.
- **Gaps:** the term now has a long list in one sentence ("or ... or ... or"); "held out of band" is not defined (the API's `result@link` and the schema's `resultLink` are two different things: one per observation, one per data stream); `size-limit` tests the declared count, so a schema with no element count still passes (review finding); the term Note was not changed.

## Rule conflict 1: failures during clean-up, 2026-11-24

From the review (an exit action cancelled from outside or reaching its time limit during clean-up had no handling in `clean-up-failure`, though `clean-up-record` counts both and `action-failure` would start a second clean-up). The owner chose **reword as proposed** (alternatives were without the last clause, and rewording first).

- **Reworded in place (`status: proposed`):** `/req/executor-run/clean-up-failure` now reads "An executor SHALL, when the command of an exit action is rejected, fails, is cancelled by a party other than the executor, or cannot be sent, or when an exit action reaches its time limit, during clean-up, perform the remaining exit actions and end the run with the ending it had already decided, and SHALL NOT treat that failure under /req/executor-run/action-failure." Its test gained two steps (a cancelled exit action, an exit action that reaches its time limit) and a check that no second clean-up starts. Gate stage 1: 384 records, no findings.
- **Still open:** whether an exit action's overrun is a failure on an ordinary transition (open since 2026-11-13); "clean-up" is still not a defined term (review finding).

## Rule conflict 2: data error against no observation, 2026-11-24

From the review: the exception in `composite-no-observation` covered more than `data-error` (a required field that is NaN or nil), and a stale observation that also omits a required field matched both rules. The owner chose **make both changes** (alternatives were change (a) only, and rewording first).

- **Reworded in place (`status: proposed`):** `/req/executor-run/composite-no-observation` ends "...except that /req/executor-run/data-error applies when the field is one the result schema does not mark optional and the value omits it or sets it to null." `/req/executor-run/data-error` now reads "...when a condition reads a field of an observation that is not older than the maximum age, the field being one that the result schema of its data stream does not mark optional and that the value omits or sets to null, ...". Tests gained a step each (a NaN or nil required field; a stale observation that omits the field). Gate stage 1: 384 records, no findings.
- **Still open:** data-error says "a condition", read as any condition including invariants and postconditions, with the cause then the data stream's name (not checked against the postcondition rules); a null in a required field is treated as omitted; a field of a never-reported stream has no observation to be "not older than the maximum age", so it stays no observation by the term, not by this sentence.

## Halt timing 1: a cancel during failure clean-up, 2026-11-24

From the review: a cancel arriving while the run cleans up after an action failure, a command failure or a data error had no stated outcome. The API: the cancel is the user's CANCELED status report on the run's command; the executor reports FAILED only after clean-up; a cancel accepted before then makes CANCELED final, and a cancel after FAILED is refused (final state). The owner chose **the halt wins; the run ends halted** (recommendation followed; alternatives were the failure standing with the halt ignored, and leaving it to the API).

- **Decided (direction):** a cancel received while clean-up for a failure is running ends the run as halted: clean-up carries on, the ending becomes halted, the status is the user's CANCELED, the cause is the innermost state as for any halt, and failed clean-up actions are still recorded. The failure that started the clean-up is not the cause.
- **Not decided:** the wording; which "innermost state" (when the cancel arrives or when the clean-up began, assumed the latter); a cancel during start checks; a cancel mid-transition.

## Halt timing 1: rule written, 2026-11-24

The owner chose **write it as proposed** (alternatives were the cause being the innermost state when the cancel arrives, and rewording first). `status: proposed`.

- **Written:** `/req/executor-run/halt-in-clean-up` ("An executor SHALL, when the command of a run is cancelled while the executor performs the exit actions required by an action failure, a command failure or a data error, end the run as halted instead of with the ending fail, and record as its cause the name of the innermost state the run was in when that clean-up began.") with a test; added to the run class and its conformance class. Gate stage 1: 386 records, no findings.
- **Gaps:** `action-failure`, `command-failure` and `data-error` still say the run ends with the ending fail and are not reworded; the new rule takes precedence by its "instead of" wording only. "When that clean-up began" is the Architect's choice, not the owner's decision. A cancel after the executor has reported FAILED is refused by the API and no rule says so. `second-halt` is untouched.
- **Still open:** a cancel during the start checks; a cancel in the middle of a transition.

## Halt timing 2: a cancel during the start checks, 2026-11-24

The owner chose **write it as proposed** (alternatives were finishing the checks and ending halted, and leaving it open). `status: proposed`.

- **Written:** `/req/executor-start/cancel-in-start` ("An executor SHALL, when the command of a run request is cancelled before every check in this class has passed, enter no state, perform no action and report no status code other than CANCELED.") with a test; added to the start class and its conformance class. Gate stage 1: 388 records, no findings.
- **Consequence stated, not in a sentence:** no run began, so no cause is recorded and no CommandResult is created (`record-in-result` says "when a run ends").
- **Gaps:** "every check in this class" is the Architect's wording; the sentence does not say the executor may stop its remaining checks; whether a request being checked counts as "in progress" for `one-run` is open; a cancel in the middle of a transition is still open.

## Halt timing 3: a cancel in the middle of a transition, 2026-11-25

The owner chose **finish the move, then halt** (alternatives were stopping at once and cleaning up what was entered, and leaving it open). `status: proposed`.

- **Written:** `/req/executor-run/halt-in-transition` ("An executor SHALL, when the command of a run is cancelled while a transition is in progress, complete that transition, then treat the cancel as a halt of the states the run is in after the transition.") with a test; added to the run class and its conformance class. Gate stage 1: 390 records, no findings.
- **Reason given:** a transition is bounded (each exit action has a time limit, entry actions are sent without waiting), so the halt is delayed only briefly, and no half-entered state needs defining.
- **Gaps:** a transition into a succeed terminal state: whether the postconditions are checked before the halt is not stated (the halt rule is silent; the Architect would read the halt as taking precedence, but this is not decided). The rule does not say whether the invariant check at the end of a transition happens before the halt. The cause follows `cause-halt` (innermost state after the transition). The "halt in progress" for `second-halt` begins when the transition completes, not at the cancel; a second cancel during the transition is not addressed.
- **Still open:** none of the halt-timing cases listed earlier remain, apart from the gaps above and the API refusing a cancel after FAILED (no rule says so).

## Halt timing 4: a cancel during a transition into a succeed terminal state, 2026-11-25

The owner chose **halted, postconditions not checked** (alternatives were checking the postconditions first and refusing the cancel, and leaving it open). `status: proposed`.

- **Written:** `/req/executor-run/halt-before-success` ("An executor SHALL, when the command of a run is cancelled while a transition into a terminal state with the ending succeed is in progress, end the run as halted instead of entering that terminal state, evaluate no postcondition, and record as its cause the name of the innermost state the run was in when that transition began.") with a test; added to the run class and its conformance class.
- **Gaps:** the cause ("when that transition began") is the Architect's choice, copied from the wording of `halt-in-clean-up`, not the owner's decision. The rule takes precedence over `halt-in-transition` ("complete that transition") by its "instead of" wording only; `halt-in-transition` is not reworded. A cancel that arrives after the terminal state is entered and the postconditions have started is not addressed (the run is then ending, and the API refuses a cancel after COMPLETED or FAILED; no rule says so). The invariant check at the end of a transition is still not placed relative to a halt.
