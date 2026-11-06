# Adversarial Review: Spec-Anchored Development Recommendation for AutonomyML

**Subject:** `docs/research/I like using spec-anchored development. I typicall.pdf` (13-page chat export; pp. 1–7 are the answer, pp. 7–12 are 192 references).
**Reviewed:** 2026-11-06.

## Summary

The PDF recommends a hybrid: OpenSpec as the change-management backbone, BMAD used selectively for analysis and review, and a standards-specific model (OGC ModSpec, Metanorma) for the standard itself. It also proposes an "AutonomyML Standards Development Profile", a separation of conformance targets, and a language-neutral conformance corpus.

**Verdict:** the direction survives, but the specific starting arrangement does not. These parts hold up:
- a thin orchestration layer around the standard
- standards-first thinking
- the three-contract split (normative language, reference implementation, development process)
- the conformance-corpus idea

This part does not: "OpenSpec backbone with requirements in OpenSpec-compatible Markdown, ModSpec later". It rests on a decision the PDF never asks about and on a capability OpenSpec doesn't have.

The PDF has no title, date, author or model attribution, and page 1 opens with the user's own prompt, so its provenance is weak.

## Findings, ranked by whether they change the recommendation

### 1. The "simplest arrangement" cannot deliver what it promises (pp. 3, 5)

- **Claim:** "Keep authoritative requirements in OpenSpec-compatible Markdown, add stable requirement identifiers and standards metadata…". Page 3 also lists "stable identifiers, requirement classes, dependencies, target types".
- **Evidence** (`openspec.dev/docs/schemas/spec-driven`, `.../configuration/change-metadata`):
  - Requirements are identified only by header text, `### Requirement: <name>`. MODIFIED headers must match exactly, and `RENAMED` uses FROM/TO.
  - The documented `x-` metadata keys are per change, in `.openspec.yaml`. They are not per requirement.
  - IDs, classes, dependencies and target types therefore have no supported home. A header-embedded ID would break on any rename.
- **Fix:** state plainly that Markdown-first means the ID is part of the header, with explicit rename rules. Otherwise go structured from day one.

### 2. The deciding question is never asked: is OGC submission the goal? (p. 5)

- The PDF says "I would start with the first unless formal publication requirements already justify the second", but never asks whether they do.
- The repo is deeply OGC-shaped: CS API, SensorML 3.0, SWE Common, and `docs/research/README.md` frames the work against OGC.
- If submission is the target, Metanorma/ModSpec is close to mandatory. Page 1 also calls ModSpec "the foundation" while the recommendation defers it, which is a tension.
- Migrating later, after IDs and structure have settled in Markdown, is the expensive path. The PDF understates that cost.
- **Fix:** ask first. If the answer is "yes or likely", flip the default.

### 3. The repo already breaks the PDF's own rule, and the PDF misses it (p. 5)

- **Rule:** "Never maintain two independently editable copies of the same normative requirement."
- **Evidence:** parsing the JSON blocks in `docs/research/asl-and-open-standards-precedents.md` shows five of the six `examples/**/*.json` files are semantically identical to embedded blocks. Only `guarded-waypoint-navigation.ugv-alpha-01.binding.json` has no embedded twin.
- **Fix:** make `examples/` authoritative and have the research doc include or link to those files.

### 4. The PDF's claims about the repo are partly right but shallow (pp. 2, 5–6)

- **Right:** the Overview separates Part 1 specifications from Part 2 bindings, and the runtime doc describes a Go/`semengine` implementation.
- **Missed:**
  - `grep` finds zero `SHALL`/`MUST`/`SHOULD` in the Overview and both research docs. There is no normative language yet.
  - `reference-runtime-module-boundaries.md` states semantics declaratively alongside Go specifics, for example §2.2/§4.4: "Every AutonomyML actuation step dispatches an asynchronous CS API command, remains `RUNNING` past `201 Created`…". That is the normative/reference-implementation blur the PDF warns about, and it never names it.
- **The pilot is not greenfield:** the PDF pitches "command acceptance versus completion" as the first slice and "a proposed requirement — not a claim about the current standard". That slice is already §4.4 of the runtime doc ("Command Accepted ≠ Action Completed"). The examples already carry `maxObservationAgeSeconds` and `sustainDurationSeconds`, so several of the PDF's "must resolve" questions are partly answered in draft.
- **Fix:** start the pilot from that existing text and extract it into normative form.

### 5. The evidence base is mostly padding (pp. 7–12)

- **Inline coverage:** only about refs [1]–[13] are cited in the text, and the PDF export detached the markers from their sentences. Most claims can't be tied to a source.
- **Irrelevant entries:**
  - [27] SailPoint, [28] CData, [29][31] Creatio, [30] Agno, [34] dbt
  - [33] a Crunchbase URL with a garbled `/page/19//page/2//…` path
  - [45] EU AI Act, [75] an "effective field theory" paper
  - [78] Merriam-Webster, [79] autonomy.com, [80] Wikipedia "Autonomy"
  - [69] UTS autonoml, [71] automl.org
- **Likely cause (unconfirmed):** the prompt on p. 1 says `https://autonomy.mil`, but the repo's `CNAME` is `autonomyml.org`. That mismatch plausibly sent retrieval toward "autonomy" and AutoML results.
- **Third-party sourcing:** the OpenSpec customization claims are sourced to third-party blogs [11][12]. The primary docs [87][113] are in the list but not cited at those claims.

### 6. Unverified or loosely supported specifics

- **Checked and correct:**
  - ModSpec Part 1: Core v1.1 — OGC 08-131r7, publication date 2026-05-21, approval date 2026-03-05, matching "published in May 2026".
  - OpenSpec supports project-local custom schemas in `openspec/schemas/`, and archive merges only specific delta structures.
  - BMAD supports custom modules.
- **Weak:** "BMAD … requirements-traceability support" (p. 3) is cited only to the repo root [3]. The official TEA module advertises "traceability", but I couldn't confirm that means requirements-to-test traceability.
- **Unchecked:** "BMAD explicitly supports carrying its planning artifacts into an existing delivery workflow" (p. 3).
- **Unmentioned:** ModSpec Parts 2 and 3 (24-065r1, 24-066r1). The PDF never says whether they matter.

### 7. The comparison table is unsourced opinion (p. 3)

- "BMAD alone: viable with substantial customization, but not my first choice" and "OpenSpec alone: the strongest lightweight starting point" carry no comparative evidence. The only hedge is the line "recommendations, not claims".
- The only head-to-head sources in the list are anecdotal: Reddit [49][51] and an "I tested three tools" blog [44].

### 8. Dated precedent (pp. 1, 4)

- The W3C "Specification Guidelines" are the QA Framework. The URLs visible in the list ([55][56][58][112]) date from 2002–2004. Final status and whether the working group is still active were not checked.
- The checklist content is likely still useful, but the PDF presents it as current guidance.

### 9. Omissions that matter for this repo

- **OGC Building Blocks** ([82][83]) are in the reference list but never evaluated. They fit JSON-Schema-plus-examples specifications, which is what `examples/` is.
- **The Serverless Workflow CTK** ([57]) is a direct conformance-kit precedent. The repo already studies that ecosystem.
- **The Layer 1/2/3 model** in `docs/research/README.md` is not mapped onto requirement classes or profiles.
- **Normative dependencies** are not addressed: versioning of CEL, SWE Common, SensorML and CS API.
- **The conformance-target list on p. 5 is incomplete.** It omits the gateway/protocol-bridge role and the `semvocab`/SHACL validation layer, both central in the runtime doc.

## Suggested next steps

1. Decide whether OGC submission is a goal (finding 2). That decision flips the default tooling choice.
2. Make `examples/` the single source for the example JSON and remove the duplicate blocks from the research doc (finding 3).
3. Draft the Standards Development Profile as a short document. Include an ID scheme that works with whichever source format step 1 selects (finding 1).
4. Extract §4.4 of the runtime doc into a first normative requirement set and treat it as the pilot (finding 4).
5. Evaluate OGC Building Blocks and the Serverless Workflow CTK before committing to a toolchain (finding 9).

## Method and caveats

- PDF text was extracted with `pypdf` (installed in a scratchpad venv) and read without rendering pages, so figures and layout were not reviewed.
- `asl-and-open-standards-precedents.md` (about 58 KB) was not read line by line. The duplication check was programmatic.
- Only the load-bearing external claims were verified (ModSpec version, OpenSpec delta/metadata handling, BMAD modules), not all 192 references.
