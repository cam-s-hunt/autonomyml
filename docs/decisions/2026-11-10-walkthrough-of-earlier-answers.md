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
