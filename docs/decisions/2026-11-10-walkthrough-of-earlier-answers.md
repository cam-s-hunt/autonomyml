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
