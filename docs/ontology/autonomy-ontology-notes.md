# Autonomy ontology: working notes

Status: working notes, started 2026-11-10 by the ModSpec Architect from the owner's decisions and the research reports in `_bmad-output/`. **This is not an ontology and not normative text.** Nothing here has an IRI, namespace or identifier. Definitions quoted from sources are the sources' words; everything marked *Architect's reading* is inference. Decisions are in `docs/decisions/2026-11-10-walkthrough-of-earlier-answers.md`.

## 1. Direction (owner decisions, 2026-11-10)

- The standard gets **its own domain ontology**, extending BFO and CCO, with SOSA/SSN terms used for concepts taken from SensorML and the Connected Systems API.
- **Mapping priority:** BFO/CCO first, SOSA second. For SOSA/SSN terms the **default route is the W3C SOSA/SSN 2023 Edition BFO/CCO alignment module** (WD section 7.1.3, non-normative, work in progress), used as an **alignment source**: the normative reference stays the 2017 Recommendation, the ontology translates the module's 2023 IRIs (`sosa:System`) to the 2017 ones (`ssn:System`) where they differ, records each correspondence, and cites the module informatively as work in progress (owner decisions, 2026-11-10). Research: `_bmad-output/research-ssn-bfo-cco-mapping.md` (section 5.1).
- **Pins:** CCO is pinned to release `v2.2` and will be adapted later (see section 9). SOSA/SSN is the 2017 Recommendation.
- **Terminology:** the standard says **capability specification** and **capability binding**, not bare "capability". The examples already use `kind: CapabilitySpecification` and `kind: CapabilityBinding`. Whether the bare word "capability" is defined at all (for example as an ability) is not decided.
- **Behavior is information:** a behavior (the content of a capability specification) is treated as an information content entity carried by something, and a system's ability to run it is a separate notion.
- **Informative, not imported:** the three ontologies named in section 8 are cited informatively and not imported.

## 2. Authority, delegation and boundaries (to be captured as ontology terms)

The research found these to be the center of nearly every definition of autonomy, and found no formalisation of them in BFO/CCO terms (`research-autonomy-ontologies.md` section 3.3, gap 2). They match the standard's own concerns: executors, human-authority gates, custody leases and `onHaltAction` preemption in the bindings. The executor *definition* deliberately leaves leases and human-authority gates out (answer 3.5), so these terms are candidates for requirements and ontology terms, not for the executor definition.

Source concepts to capture (the sources' wording, shortened; see the report for URLs and tags):

| Concept | Source wording or framing | Source |
|---|---|---|
| Delegation within boundaries | "Autonomy results from delegation of a decision to an authorized entity to take action within specific boundaries." | Defense Science Board 2016 Summer Study |
| Human independence | Autonomy characterized "from the perspective of Human Independence (HI), the inverse of HRI"; Contextual Autonomous Capability; three axes: mission complexity, environmental complexity, human independence | NIST SP 1011 (ALFUS) |
| Without human intervention | "ability to perform intended tasks based on current state and sensing, without human intervention" | ISO 8373:2021 3.2 |
| Self-modifiable goal or domain | "capable of modifying its intended domain of use or goal without external intervention, control or oversight" | ISO/IEC 22989:2022 3.1.5; EASA AI Roadmap 2.0 |
| Authority | "The ability to make decisions and take actions without the need for approval from another member involved in the operations"; authority scale: directed, supervised, safeguarded, non-supervised | EASA AI Roadmap 2.0; EASA Concept Paper Issue 02 |
| Who selects and engages | autonomous, semi-autonomous and operator-supervised autonomous weapon systems | DoDD 3000.09 (2023), weapon systems only |
| Operational design domain (boundaries) | the domain in which a function is designed to work; DDT fallback and minimal risk condition | SAE J3016 |
| Authority Role, Process Regulation | CCO v2.2 terms for who may assign roles and what a process is required, prohibited or permitted to do | CCO v2.2 (see section 6) |
| Variable autonomy / playbook | a human calls a play, a commander changes it; roles assigned to human and non-human team members | OPTaC; Miller et al. 2005 |
| Function allocation levels | ten levels of computer assistance; four stages with levels each | Sheridan and Verplank 1978; Parasuraman, Sheridan and Wickens 2000 |

Candidate ontology terms *(Architect's reading, names not proposed)*: a delegation of a decision or action from one agent to another; the boundaries or domain within which a delegation holds; the authority to approve, override or halt; a human-authority gate; a custody lease; a preemption or halt action; an interval or scope for a delegation. The sources disagree on whether levels of autonomy are meaningful (`research-autonomy-ontologies.md` section 3.2), so levels are a reporting scheme to decide later, not a core term.

## 3. State

The ontology must define **state** itself (owner, 2026-11-10). Direction already chosen (answer 3.6): a state is a **control mode of an automaton**, kept distinct from **system state** (the world's or system's condition) and from **node status** (a behavior-tree return value); the six example types (`csapiCommandAction`, `succeed`, `fail`, `mode`, `behaviorTree`, `choice`) become kinds of state under it. Wording is the owner's.

Evidence to carry over (`research-state-and-control-models.md`): no shared definition of "state" exists (three senses: model element, condition of the world or system, ontological occurrent); BFO 2020 has no "state"; CCO has `Stasis`, a kind of process; SOSA/SSN has no state class; OPTaC has none. The labelled-transition-system definition (Henzinger) is the lowest common abstract definition the report found. Terminal states: two endings stand, a third (cancelled or halted) is blocked on the halt-behavior design question (answer 3.8).

## 4. Behavior as information carrier

Working pattern *(Architect's reading of the owner's decision and `research-cco-capabilities.md`)*:

- A **capability specification** is information: it describes a behavior and exists whether or not any system can run it. In CCO terms, the nearest classes are Plan, Algorithm and Performance Specification, which are specifications that `prescribe` acts, with the document as the information bearing entity that carries it.
- A **capability binding** is information that ties a specification to the resources of a particular system.
- A system's **ability to run** a specification is a separate notion, borne by the executing system, and related to the specification by `concretizes`. CCO's Agent Capability is a realizable entity of a *material* bearer, so the bearer is the executing hardware-software system, not the software on its own.
- Known issue: `prescribes` relates instances, which clashes with a specification that has no executor. A digital-twin paper cited in the report proposes class-level prescription (OWL Full) or the Modal Relation Ontology as workarounds. Not adopted.

## 5. Systems: software and virtual systems

The standard says software and virtual systems count as systems (answer 3.1). CCO's Agent is "A Material Entity that bears an Agent Capability", so software as information cannot be one. Owner's working approach, 2026-11-10: **use SOSA's `System`**, with behavior carried as information (section 4), **until the new CCO is out**.

Findings of the SSN-to-BFO/CCO research (`_bmad-output/research-ssn-bfo-cco-mapping.md`; agent-written, no reasoner run):
- SOSA/SSN itself, in both the 2017 Recommendation and the 2023 draft, has **no materiality axiom** for System and states that software and virtual systems are in scope. The 2023 draft says `sosa:Sensor` "may be non-material - e.g. a software agent".
- The **NCOR "SSN-to-BFO" mapping** (CC0, one maintainer) makes System, Platform, Sensor, Actuator and Sampler material, so importing it wholesale would make every software-only system inconsistent or misclassified. **Not adopted.**
- The **W3C 2023 module** maps `sosa:System` to BFO independent continuant, which allows non-material systems, but BFO keeps independent continuants and generically dependent continuants (information) disjoint, so *code-only* systems still have no place as a System under it (the report's inference). The route for software is the carrier: a material computer bears a role or function that `concretizes` the code, and **neither mapping provides that link; this ontology adds it** (section 4).
- Both mappings agree that `sosa:Procedure` is a CCO Prescriptive Information Content Entity, and agree on Planned Act for the act terms and Cause for Stimulus.
- Known issues with the W3C module: a Turtle typo (`rdfs:subClassOF`) drops one axiom; it uses an unversioned CCO import and a CCO 2.1+ term (Sensing Process); it uses 2023 IRIs.

## 6. OPTaC concepts to adopt, updated to CCO v2.2

Owner: adopt OPTaC concepts, updated to the latest CCO terms. Source: Kasmier et al., *Ontology of Plays for Autonomous Teaming and Collaboration*, ONTOBRAS 2021, CEUR Vol-3050 pp. 9-22 (CC BY 4.0). **No OPTaC ontology file or IRI was found**, so the concepts are adopted from the paper's text, with attribution. Which exact terms are adopted is the owner's choice.

| OPTaC / CCO v1.3 term | CCO v2.2 | Note |
|---|---|---|
| Plan: "a Directive Information Content Entity that prescribes some set of intended Intentional Acts..." | Plan, a **Prescriptive** Information Content Entity ("Directive ICE" kept as an alternative label) | |
| Intentional Act | **Planned Act** ("Intentional Act" kept as an alternative label) | |
| Action Regulation | no class of that name; **Process Regulation** has the same definitional shape | the successor link is the report's inference |
| Authority Role | present; now realized by processes that create, modify, transfer or eliminate Process Regulations or other Authority Roles | |
| Act of Affiliation | no class of that name; **Act of Association** is the nearest | the successor link is the report's inference |
| Information Content Entity | unchanged | |
| Team, Team Member Role | OPTaC definitions, not military-specific | Team Member Role depends on Action Regulation |
| Plan structure (OPTaC Figure 1) | Play is a Plan with parts that prescribe an objective, means (intentional acts) and roles realized by those acts | reusable pattern |
| Goal: "an Entity which is prescribed by some Objective" | Objective is a CCO class | |

Open items on this adoption: OPTaC's **Play** requires a competitive context (`in_competition_with`), which excludes non-adversarial behavior, so adopting Play unchanged needs a decision; the military taxonomy of play types (Effects, Intelligence Gathering, Sustainment, Movement) is Army-doctrine-derived and military-specific; the paper has no state, task or mission class; CCO v2.2 has no Mission, Task or Activity class.

## 7. Mission specification patterns: inspiration for states and behavior-tree primitives

Owner: take the mission specification patterns as inspiration for states and behavior-tree primitives. Source: Menghi et al., "Specification Patterns for Robotic Missions", IEEE Transactions on Software Engineering (DOI 10.1109/TSE.2019.2945329); read from the arXiv v1 preprint https://arxiv.org/abs/1901.02077 and the catalogue https://www.roboticpatterns.com/ (the IEEE version was not read). Full extraction, with the LTL/CTL templates and source inconsistencies, is in `_bmad-output/research-mission-patterns.md`. Licence: the paper's arXiv terms were not checked here; the catalogue states "(c) 2018" and no licence; the companion tool PsALM has no licence. Treat as inspiration with attribution, not as text to copy.

**What the catalogue is.** 22 patterns in three groups, each with an intent, LTL and CTL templates, variations, relationships and a Buchi automaton. It describes properties a behavior must satisfy (what), not controller structures (how). It says nothing about behavior trees, finite state machines, statecharts or SCXML.

| Group | Patterns | Idea |
|---|---|---|
| Core Movement (10) | Coverage: Visit, Sequenced Visit, Ordered Visit, Strict Ordered Visit, Fair Visit. Surveillance: Patrolling, Sequenced, Ordered, Strict Ordered, Fair Patrolling | reach a set of locations, once (coverage) or repeatedly (surveillance), with increasing constraints on order and fairness |
| Avoidance (6) | Past, Global and Future Avoidance; Upper, Lower and Exact Restricted Avoidance | something must not happen: always, after an event, until a condition, or more or fewer than n times |
| Triggers (6) | Instantaneous, Delayed, Prompt and Bound Reaction, Bound Delay; Wait | a stimulus triggers a response at the same step, the next step, eventually, or if-and-only-if; or inaction until a stimulus |

**Observation model (useful for postconditions).** Patterns are templates over three kinds of proposition, evaluated over a discrete-step trace: location propositions (a robot is in a place), environment-condition propositions, and action-execution propositions (a robot is performing an action). This is a ready small vocabulary for guards and postconditions "over observations" (answer 3.7). The tables assume one robot, and time, space and probability are future work in the paper.

**Candidate primitives, as options only (Architect's reading; the report marks all of it inference):**
- *State kinds and transitions:* a "wait" state kind (remain until a condition); a visit-sequence region versus a looping patrol region; a transition-timing vocabulary taken from the trigger patterns (same-step, next-step, eventually, iff-bound); an optional occurrence-count attribute (at most, at least, exactly n).
- *Behavior-tree nodes:* sequence over "reach location" actions, with the order variants being what a plain sequence does not express; repeat-forever and counter decorators; run-until decorators for wait; guard decorators enabled after an event; always-evaluated invariant conditions; condition-guarded actions for reactions, with a delayed reaction needing memory of a pending obligation.
- *Postconditions and guards:* named, parameterised constraint forms for requirements, for example a reaction contract (stimulus, response, timing), an invariant, a scoped invariant, a bounded-occurrence constraint, and an ordered-coverage constraint.

**Cautions.** The paper's own Table II and Fig. 2 disagree on Strict Ordered Patrolling (four versus three conjuncts); the catalogue site has apparent copy-paste errors (the Wait intent, some tags, the Sequenced Visit CTL); "Prompt Reaction" is "Fast Reaction" in the paper's Fig. 1. Any template taken from it needs checking against the paper.

## 8. Cited informatively, not imported

Owner: do not literally import those three, cite them informatively. Owner confirmed "those three" as: SkiROS2 (skills with pre, hold and post conditions, a close match to the postcondition concept), SOMA (capability as a disposition, with Task, Plan, Goal), and OMG ROSO 1.0 (Capability, Function, Agent, not BFO-aligned), which were listed together in the discussion. **Confirmed by the owner.** Licences noted in the research: SOMA LGPL-3.0, SkiROS2 LGPL-3.0-or-later, ROSO OMG Non-Assert IPR.

## 9. Pins and what to adapt later

- **CCO:** release tag `v2.2`, published 2026-08-14, tag commit `0bc7d33e1bc09fd4693366119ab4e03cb0340042`, BSD-3-Clause; asset checksums are in `_bmad-output/research-edition-pins.md` (merged TTL SHA-256 `a9453382b25b40781c181d6ba44981f228abb76d90d548846713adba9baadb42`). CCO IRIs redirect to the moving `develop` branch, so the tag and checksum are what is pinned. CCO 3.0 is planned by 2026-12-31 and 4.0 by 2027-06-30, and the CCO Governance Board advises users to wait for 4.0 (research report, not independently checked). Owner: pin the current release and adapt later.
- **SOSA/SSN:** the 2017 Recommendation; a 2023 Edition draft is in progress.

## 10. Open questions

- Whether bare "capability" is defined (as an ability) and whether the identifier's type segment becomes `capability-specification`.
- The software-system approach beyond SOSA `System`, once the mapping research is in.
- Which OPTaC terms exactly, and what to do about Play's competitive context.
- The authority and delegation terms: names, definitions and which become requirements.
- Whether the ontology's IRIs and the standard's document namespace are the same thing (they are separate: the document namespace is the gate config's `namespace`, still empty).
