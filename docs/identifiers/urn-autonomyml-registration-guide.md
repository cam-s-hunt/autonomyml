# Guide: registering the formal URN namespace identifier `autonomyml` with IANA

Prepared 2026-11-10 from public primary sources. Every factual claim carries an inline URL. Anything not confirmed from a source is marked **UNVERIFIED**.

## 1. Purpose and status

This is a guide for the owner of the AutonomyML standard. It explains how a person can ask IANA to register a formal URN namespace identifier (NID) and what the owner must decide and supply along the way. **Nothing has been submitted, emailed, posted or requested; no account was created; no information about the owner or the project was sent to any service** (the only lookup that used the draft name was one public web search for the bare string `autonomyml`). Registration is the owner's action and the owner's decision. Where this guide shows template fields, every commitment (registrant, persistence, assignment rules, resolution, security) is left as `OWNER TO DECIDE`; the assistant cannot answer those.

Why it matters: a name beginning `urn:` is not automatically a URN. RFC 8141 says "The syntactical correctness of a name starting with 'urn:' is not sufficient to make it a URN," and the NID "needs to be registered in accordance with the rules defined here" ([RFC 8141 section 1](https://www.rfc-editor.org/rfc/rfc8141#section-1)). Until registered, `urn:autonomyml:...` is not a valid URN under that RFC.

Sources read: the plain-text RFCs 8141, 5165, 6963, 7467, 8069 and 4151 from rfc-editor.org (RFC 8141 sections 1 to 7, Appendices A to C were read in full; section 3.2 examples and the reference lists were skimmed); the IANA registry page and its XML; three completed IANA template files; OGC Naming Authority Procedures 09-046r6; and two public IETF list-archive messages used only for process facts. Fetched content was treated as data, not instructions.

## 2. Is a formal NID the right kind?

### 2.1 The three kinds

| Kind | What it is | Source |
|---|---|---|
| Formal NID | The registrant proposes the NID string; the policy is Expert Review; the namespace should benefit some Internet users, and the assigning organization SHOULD meet stability, competency and non-reassignment criteria. | [RFC 8141 section 5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1), [section 6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2) |
| Informal NID | A full URN namespace, but "the registrant does not designate the NID; instead, IANA assigns" a string `urn-` plus the next number (for example `urn-7`). | [RFC 8141 section 5.2](https://www.rfc-editor.org/rfc/rfc8141#section-5.2) |
| `urn:example` | A registered formal NID "for use in documentation and in URN-related testing and experimentation"; not for building higher-level applications. | [RFC 6963 section 1](https://www.rfc-editor.org/rfc/rfc6963) |

The informal and formal kinds differ by "the expected level of service, the information needed to define the URN namespace, and the procedures for registration" ([RFC 8141 section 5](https://www.rfc-editor.org/rfc/rfc8141#section-5)). Both kinds go through "Expert Review, per Section 6 of RFC 8141" according to the [IANA registry page](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml). Because the owner wants a name that reads `urn:autonomyml:...`, only the formal kind lets the owner propose that string; an informal registration would be `urn-<number>` instead. Whether formal registration is *appropriate* is the owner's judgement; the RFC's own bar is that the namespace "provides benefit to some subset of users on the Internet" and is not limited to a community "not connected to the Internet" ([RFC 8141 section 5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1)). RFC 8141 also says the organization assigning names SHOULD show organizational stability, competency in assignment, and a "commitment to not reassigning existing URNs" (same section).

### 2.2 The RFC's syntax tests, applied to `autonomyml`

Tests from [RFC 8141 section 2](https://www.rfc-editor.org/rfc/rfc8141#section-2) (grammar: `NID = (alphanum) 0*30(ldh) (alphanum)`, so 2 to 32 characters, letters, digits and hyphens, no hyphen at either end) and [section 5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1):

| Test | Source | `autonomyml` |
|---|---|---|
| ASCII alphanumerics and hyphen only; starts and ends with alphanumeric; 2 to 32 characters | section 2 grammar | Pass (10 characters, all ASCII letters). |
| NID is case insensitive (`autonomyml` and `AutonomyML` are equivalent) | [section 2.1](https://www.rfc-editor.org/rfc/rfc8141#section-2.1) | Applies; the registered form should be given in lowercase (suggestion, not an RFC rule). |
| "MUST NOT be an already-registered NID" | section 5.1 item 1 | Pass as of 2026-10-28 (see 2.3). |
| "MUST NOT start with 'urn-'" | section 5.1 item 2 | Pass. |
| "MUST be more than two characters long, and it MUST NOT start with ALPHA ALPHA '-'" (two letters then a hyphen, reserved for ISO 3166 alpha-2 based NIDs); also no `xn--` or any two letters plus two hyphens | section 5.1 item 3 | Pass: begins `aut`; the third character is a letter, not a hyphen. |
| "MUST NOT start with the string 'X-'" | section 5.1 item 4 | Pass. |
| Avoid strings that could be "construed as identifiers for, or registered under the authority of, countries (including ISO 3166-1 alpha-3 codes)" or imply association with existing URI schemes, non-URN identifier systems, or trademarks | section 5.1, last paragraph | Not a country code. Trademark and association check **UNVERIFIED**: I ran one public web search for the exact string and found no product named `autonomyml`; the nearest result was a monograph titled "AutonoML" in search-result listings ([nowpublishers MAL-093](https://nowpublishers.com/article/DownloadSummary/MAL-093), [catalyzex](https://www.catalyzex.com/paper/autonoml-towards-an-integrated-framework-for)); I did not open those pages. It is similar but a different string. This is not a trademark search; the owner should do their own. |

The RFC adds that disputes about "ownership" of strings are "disagreements among the parties involved; neither IANA nor the IETF will become involved in such disputes except in response to orders from a court of competent jurisdiction" ([section 5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1)).

### 2.3 Is it already registered?

I fetched the [IANA "Uniform Resource Names (URN) Namespaces" registry](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml) (and its [XML form](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xml)) on 2026-11-10. The page shows **"Last Updated 2026-10-28"**. A case-insensitive search of the full page and XML for `autonomyml` found **no match** in either the Formal or the Informal table. The formal table lists, among others, `example` ([RFC 6963](https://www.rfc-editor.org/rfc/rfc6963)), `ogc` ([RFC 5165](https://www.rfc-editor.org/rfc/rfc5165)), `nato` ([RFC 7467](https://www.rfc-editor.org/rfc/rfc7467)) and `ieee` ([RFC 8069](https://www.rfc-editor.org/rfc/rfc8069)). The highest informal entry listed is `urn-8` (registered 2025-07-02). Registrations made after 2026-10-28 would not appear in what I read, and the owner should re-check the live registry just before submitting.

The page itself states the registration procedure only as "Expert Review, per Section 6 of RFC 8141. Fast-track procedure for standards organizations described in Section 6.3," names five designated experts (Peter Saint-Andre as team leader, Dale Worley, Juha Hakala, Stephanie Nitsche, Lars Svensson) and does **not** state a mailing list, submission form, or contact address in the registry text.

## 3. Prerequisites the RFC asks for

The RFC says the formal policy is Expert Review and that "a specification (as distinct from the registration template) is not strictly required," but registrants "SHOULD provide a stable specification documenting the URN namespace definition," because it lets them "clearly formulate their 'contract' with the intended user community" ([RFC 8141 section 6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). The template can be part of an Internet-Draft "or a specification in another series, although that is not a requirement" (same section). A list-archive message from a designated expert states that "publication of an Internet-Draft or RFC is not required for registration of a URN namespace identifier" ([IETF `urn` list archive, Nov 2022](https://mailarchive.ietf.org/arch/msg/urn/9WARfIqddxTmm3Gia6xPctL36d8/)).

A namespace definition SHOULD address its purpose, URN syntax (including any r-/q-component use), the assignment process, security implications, interoperability issues, and optionally the resolution process ([RFC 8141 section 6.1](https://www.rfc-editor.org/rfc/rfc8141#section-6.1)).

| Prerequisite | What the RFC requires or asks | Who supplies it |
|---|---|---|
| Specification document | Community route: SHOULD be stable and expand on the template issues ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). Fast-track route: "A specification is required that reflects or points to the needed external standards or specifications" ([6.3 item 2](https://www.rfc-editor.org/rfc/rfc8141#section-6.3)). A pointer goes in the template's Documentation field ([App. A](https://www.rfc-editor.org/rfc/rfc8141#appendix-A)). | **Owner.** Must exist at a stable location; the assistant cannot decide where it is published. |
| Registrant identity | "The person or organization that has registered the NID," with name and address of the registering organization plus name and contact (email, phone or postal) of the designated contact ([App. A](https://www.rfc-editor.org/rfc/rfc8141#appendix-A)). The registrant and contact appear publicly in the IANA record (the [registry page](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml) has a Contact Information table, and the [`wmo` template](https://www.iana.org/assignments/urn-formal/wmo) shows registrant and contact in the published file). | **Owner.** Whether to register as an individual, a project or an organization is the owner's decision. |
| Persistence commitment | Names are "never reassigned to a different resource ... even if the name itself is deprecated or becomes obsolete" ([section 5](https://www.rfc-editor.org/rfc/rfc8141#section-5)); organizations SHOULD show stability and a plan if they can no longer maintain the namespace ([5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1)). | **Owner.** A binding commitment; only the owner can make it. |
| Assignment process | Who assigns names, whether assignment is open, closed or delegated, and how uniqueness is ensured ([6.4.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.3)). | **Owner.** |
| Resolution | Template MUST say "whether resolution mechanisms are intended or anticipated" ([6.4.6](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.6)). "Not planned" is an accepted style of answer in completed templates (see 4.10). | **Owner.** |
| Uniqueness | "Unique, assigned in a consistent way, and assigned according to a common definition" ([section 5](https://www.rfc-editor.org/rfc/rfc8141#section-5)). | **Owner** designs and commits to it. |
| Lexical equivalence | Rules for URN-equivalence beyond the default procedure; they must only remove false negatives and never contradict the default ([6.4.2 item 3](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.2), [3.1](https://www.rfc-editor.org/rfc/rfc8141#section-3.1)). | **Owner** decides (for example, whether the NSS is case-insensitive). |
| Fast-track authorization (only if used) | Applies "in situations in which the registration request originates from, or is authorized by, a recognized standards development organization, scientific society, or their designees"; the body must request registration from IANA when satisfied, and "decisions about whether to recognize the requesting entity as a standards development organization or scientific society are the responsibility of the IESG" ([6.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.3)). The template must clearly indicate fast-track status in the Registrant field. | **Owner.** I make no judgement on whether the owner or any body qualifies, and found no published list of recognized bodies (**UNVERIFIED**). |

## 4. The registration template, field by field

The template is [RFC 8141 Appendix A](https://www.rfc-editor.org/rfc/rfc8141#appendix-A). It has 13 fields. A designated expert on the list asked a requester to "format the registration request in accordance with Appendix A of RFC 8141," saying this "will expedite the process" ([IETF `urn` list archive, May 2024](https://mailarchive.ietf.org/arch/msg/urn/gwtk0GIeqoI2C7d9NntrxENbwDE/)). A request whose template followed the older RFC 2141 format was told to update it ([Nov 2022 message](https://mailarchive.ietf.org/arch/msg/urn/9WARfIqddxTmm3Gia6xPctL36d8/)).

**Important: the RFC examples you were asked to read use the older template.** RFC 5165 (`ogc`), RFC 6963 (`example`), RFC 7467 (`nato`) and RFC 8069 (`ieee`) were written under RFC 3406, which RFC 8141 obsoletes ([RFC 8141 section 1](https://www.rfc-editor.org/rfc/rfc8141#section-1)). Their field names differ. Examples below therefore come mainly from IANA template files that use the RFC 8141 layout ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo), [`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart), [`cdx`](https://www.iana.org/assignments/urn-formal/cdx)), with the four RFCs as secondary examples. All examples are non-binding illustrations of the *kind* of content, not wording to copy. Third-party contact details are deliberately omitted.

Mapping from the old (RFC 3406-era) field names seen in the four RFCs to where the same topic lives in the RFC 8141 template (this mapping is my reading of the RFC text; RFC 3406 itself was not read):

| Old field (as seen in RFC 5165/6963/7467/8069) | Where it goes in RFC 8141 |
|---|---|
| Declared registrant | Registrant |
| Declaration of syntactic structure | Syntax |
| Rules for lexical equivalence | Syntax ([6.4.2 item 3](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.2)) |
| Conformance with URN syntax | Syntax ([6.4.2 item 4](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.2)) |
| Process of identifier assignment; Identifier uniqueness considerations | Assignment ([6.4.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.3)) |
| Process for identifier resolution | Resolution |
| Relevant ancillary documentation | Documentation |
| Scope | Purpose ([6.4.1 item 2](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.1)) |
| Identifier persistence considerations; Validation mechanism | No dedicated field in Appendix A. Persistence is a section 5 / 5.1 expectation; the owner may address it in Purpose, Assignment or Additional Information (suggestion). |

### 4.1 `Namespace Identifier`
- RFC text: "Requested of IANA (formal) or assigned by IANA (informal)."
- Plain English: the NID string you are asking for.
- Value: `OWNER TO DECIDE` (draft candidate: `autonomyml`).
- Example: `wmo` template: "Namespace Identifier: wmo" ([IANA](https://www.iana.org/assignments/urn-formal/wmo)).

### 4.2 `Version`
- RFC text: "The version of the registration, starting with 1 and incrementing by 1 with each new version."
- Plain English: 1 for a first registration.
- Value: `OWNER TO DECIDE` (the RFC implies 1 for a first submission).
- Example: all three IANA templates read use "Version: 1" ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo), [`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart), [`cdx`](https://www.iana.org/assignments/urn-formal/cdx)).

### 4.3 `Date`
- RFC text: "The date when the registration is requested of IANA, using the format YYYY-MM-DD."
- Plain English: the date you send it.
- Value: `OWNER TO DECIDE` (date of submission).
- Example: `stalwart`: "Date: 2025-04-14" ([IANA](https://www.iana.org/assignments/urn-formal/stalwart)).

### 4.4 `Registrant`
- RFC text: "The person or organization that has registered the NID, including the name and address of the registering organization, as well as the name and contact information (email, phone number, or postal address) of the designated contact person. If the registrant is a recognized standards development organization, scientific society, or similar body requesting the fast-track registration procedure (see Section 6.3), that information should be clearly indicated in this section."
- Plain English: who is accountable for the namespace and who to contact, and whether you are claiming fast track.
- Value: `OWNER TO DECIDE` (registrant name; address; contact person and contact method; fast-track claim yes/no and on what basis).
- Examples: `stalwart` gives a company name, address and a designated contact person; `wmo` gives an organization, address, URL and a contact person ([`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart), [`wmo`](https://www.iana.org/assignments/urn-formal/wmo)); RFC 5165 names the Open Geospatial Consortium as "Declared registrant" with a care-of contact ([RFC 5165 section 2](https://www.rfc-editor.org/rfc/rfc5165)).

### 4.5 `Purpose`
- RFC text: "Described in Section 6.4.1." That section lists seven matters: (1) the kinds of resources identified; (2) scope and applicability, including community of use and public or private networks; (3) how the community and the Internet at large benefit; (4) how the namespace relates to existing URN namespaces, URI schemes and non-URN identifier systems; (5) kinds of software that can use or resolve the URNs; (6) whether resolution services are or will be available, with q-/r-component examples; (7) whether the namespace is expected to become a constituent part of a standard in the IETF or another recognized standards body ([6.4.1](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.1)).
- Plain English: what the names identify, who uses them and why a URN is needed.
- Value: `OWNER TO DECIDE`.
- Example: `wmo`: the NID "will be used to identify resources as part of public international data and metadata exchange activities" ([IANA](https://www.iana.org/assignments/urn-formal/wmo)). `cdx` identifies a class of document (bills of materials) and shows an f-component use ([IANA](https://www.iana.org/assignments/urn-formal/cdx)).

### 4.6 `Syntax`
- RFC text: "Described in Section 6.4.2 ... Unless the registration explicitly describes the semantics of r-components, q-components, and f-components in the context of this URN namespace, those semantics are undefined." Section 6.4.2 asks for: (1) the structure of URNs (ABNF, an algorithm, a regular expression, or "opaque"); (2) special character-encoding rules; (3) URN-equivalence rules (examples: case-insensitive NSS, hyphen grouping, quote forms); (4) special considerations for conforming with URN syntax; (5) any meaning of q- or f-components ([6.4.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.2)).
- Plain English: the exact shape of `urn:autonomyml:...`, and how to tell two names are "the same".
- Value: `OWNER TO DECIDE`. (The segments after `urn:autonomyml:` are not decided anywhere in this guide.)
- Examples: `wmo` shows `urn:wmo:{resource-type}:{centre-id}:{local-id}` with each part explained; `cdx` gives a full ABNF; `stalwart` adds "string comparison of the NSS is case-insensitive" as an extra equivalence rule ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo), [`cdx`](https://www.iana.org/assignments/urn-formal/cdx), [`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart)). RFC 5165 uses `urn:ogc:{OGCresource}:{ResourceSpecificString}` and states that "OGCresource" is case sensitive ([RFC 5165 section 2](https://www.rfc-editor.org/rfc/rfc5165)). RFC 8069 states that its two strings are "case insensitive" ([RFC 8069 section 2](https://www.rfc-editor.org/rfc/rfc8069)).

### 4.7 `Assignment`
- RFC text: "Described in Section 6.4.3": mechanisms or authorities for assigning URNs (completely open such as first-come first-served, completely closed, or limited and delegated, and how one becomes an assigner), and methods for ensuring uniqueness (sequential assignment by one authority, partitioned among delegated authorities, or an algorithm that guarantees uniqueness) ([6.4.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.3)).
- Plain English: who is allowed to mint names, and what stops two names being the same or being reused.
- Value: `OWNER TO DECIDE`.
- Examples: `wmo` splits assignment by segment among the Secretariat and Members; `stalwart` separates central assignment from random 128-bit values ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo), [`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart)). RFC 7467 states the registrar "shall directly ensure the global uniqueness" and that URNs "shall be assigned to one resource at most and not reassigned," recording status as "active" or "archive" ([RFC 7467 sections 2.6 and 2.7](https://www.rfc-editor.org/rfc/rfc7467)). RFC 5165 assigns this to the OGC Naming Authority (ONA) ([RFC 5165 section 2](https://www.rfc-editor.org/rfc/rfc5165)).

### 4.8 `Security and Privacy`
- RFC text: "Described in Section 6.4.4": security and privacy issues in assignment, use and resolution, such as false negatives/positives in equivalence comparison, leakage of private information, directory harvesting ([6.4.4](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.4)).
- Plain English: what could go wrong for users or for people named by identifiers.
- Value: `OWNER TO DECIDE`.
- Example: `stalwart` lists specific considerations for its token types; `cdx` points to the UUID URN considerations and warns about what may be placed in an f-component ([`stalwart`](https://www.iana.org/assignments/urn-formal/stalwart), [`cdx`](https://www.iana.org/assignments/urn-formal/cdx)). `wmo` states "No security or privacy issues are foreseen at this time" ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo)).

### 4.9 `Interoperability`
- RFC text: "MUST specify any known potential issues related to interoperability," such as confusion with other URN namespaces, non-URN identifier systems or URI schemes because of syntax or scope; concerns that arise during registration "should be resolved as part of or in parallel to the registration process" ([6.4.5](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.5)).
- Plain English: overlaps and possible confusion with existing identifiers. Consider the similar-looking "AutonoML" observation in section 2.2 here.
- Value: `OWNER TO DECIDE`.
- Example: `cdx` explains why a UUID serial number alone is not enough to reference a BOM; `wmo` says no issues are foreseen ([`cdx`](https://www.iana.org/assignments/urn-formal/cdx), [`wmo`](https://www.iana.org/assignments/urn-formal/wmo)).

### 4.10 `Resolution`
- RFC text: "MUST specify whether resolution mechanisms are intended or anticipated"; if intended, SHOULD say whether the assigning organization will operate or recommend resolvers, list requirements for publicly advertised resolution services, and describe r-component handling ([6.4.6](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.6)).
- Plain English: do these names resolve to anything, and who provides that.
- Value: `OWNER TO DECIDE`.
- Examples: `wmo`: "A resolution service is not planned as of mid-2025; however, it is being discussed and evaluated for future capability" ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo)). RFC 5165 describes an operational OGC resolver at a stated host and says the namespace is not listed with a Resolution Discovery System ([RFC 5165 section 2](https://www.rfc-editor.org/rfc/rfc5165)).

### 4.11 `Documentation`
- RFC text: "A pointer to an RFC, a specification published by another standards development organization, or another stable document that provides further information about this URN namespace."
- Plain English: a stable URL or citation to your specification.
- Value: `OWNER TO DECIDE` (the specification's stable location; see section 3).
- Example: `wmo` cites the WMO manual and its library URL; `cdx` cites a specification overview page ([`wmo`](https://www.iana.org/assignments/urn-formal/wmo), [`cdx`](https://www.iana.org/assignments/urn-formal/cdx)).

### 4.12 `Additional Information`
- RFC text: "Described in Section 6.4.7": useful context, such as "comparisons to existing URN namespaces that might seem to overlap." The section "is optional" ([6.4.7](https://www.rfc-editor.org/rfc/rfc8141#section-6.4.7)).
- Value: `OWNER TO DECIDE` (may be omitted).
- Example: the [`wmo` template](https://www.iana.org/assignments/urn-formal/wmo) lists key documents.

### 4.13 `Revision Information`
- RFC text: "Description of changes from prior version(s). (Applicable only when earlier registrations have been revised.)" A revised registration "MUST describe differences from prior versions" ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)).
- Value: not applicable to a first registration; leave out (`OWNER TO DECIDE` if unsure).
- Example: none of the three IANA templates read is a revision, so I have no completed example.

## 5. Step-by-step submission and review

The RFC does not state a timeline, a fee, or a tracking system (**not stated in [RFC 8141](https://www.rfc-editor.org/rfc/rfc8141); UNVERIFIED elsewhere**).

1. **Confirm the name is free and passes the tests.** Re-check the [IANA registry](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml) and section 5.1 constraints (see section 2).
2. **Prepare the template and, preferably, a stable specification.** Fill the 13 fields from Appendix A ([6.2 step 1](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). Publication as an Internet-Draft or RFC is not required ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2); [expert statement](https://mailarchive.ietf.org/arch/msg/urn/9WARfIqddxTmm3Gia6xPctL36d8/)).
3. **Choose the route.** Community registration ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)) or, only if a recognized standards body requests it, fast track ([6.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.3)). Under fast track the list and expert reviews are "strictly advisory" and the body controls the time allowed. That is for the owner to decide.
4. **Send the completed template to the discussion list `urn@ietf.org`** ([6.2 step 2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). **Correction to the premise of the request:** `urn-nid@ietf.org` is not the current list. RFC 8141 says the RFC 3406 list "(urn-nid@apps.ietf.org) is discontinued and replaced by the discussion list urn@ietf.org" ([7.3](https://www.rfc-editor.org/rfc/rfc8141#section-7.3)). Archived messages show `urn@ietf.org` as the list address (`List-Post`) and the list described as "Revisions to URN RFCs" ([2024 message](https://mailarchive.ietf.org/arch/msg/urn/gwtk0GIeqoI2C7d9NntrxENbwDE/)). The owner would need to follow the list's own subscription and posting rules; I could not open the list-information page (HTTP 403 for the Mailman 3 page), so whether non-members can post is **UNVERIFIED**. The public archive is at [mailarchive.ietf.org/arch/browse/urn](https://mailarchive.ietf.org/arch/browse/urn).
5. **Expert Review.** The Designated Experts and list participants review. "If necessary to address comments received, repeat steps 1 and 2" ([6.2 step 3](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). Registrants and experts "are strongly encouraged to work together in a spirit of good faith and mutual understanding to achieve rough consensus," and experts are expected to avoid "race conditions" on proposed NIDs during long iterations ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)).
6. **Objections.** The RFC defines no formal appeal. Comments are handled by revising and resending (step 5). Disputes over who "owns" a string are left to the parties; IANA and the IETF intervene only on a court order ([5.1](https://www.rfc-editor.org/rfc/rfc8141#section-5.1)). Whether an expert can refuse outright is not stated (**UNVERIFIED**).
7. **Approval and IANA entry.** "If the Designated Experts approve the request and no standardization action is involved, the IANA will register the requested NID" ([6.2 step 4](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). If standardization is anticipated, the experts write a report to the approving body and IANA registers only after directions from that body ([same step](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)). In the fast-track route, the body's representatives request IANA to complete registration ([6.3 step 4](https://www.rfc-editor.org/rfc/rfc8141#section-6.3)). In an archived 2022 case the expert reported "I've asked IANA to register this namespace" ([archive](https://mailarchive.ietf.org/arch/msg/urn/9WARfIqddxTmm3Gia6xPctL36d8/)). The IANA page does not describe a requester-facing form for NIDs. IANA has a generic [General Request for Assignments form](https://www.iana.org/form/protocol-assignment); whether it is used for NIDs is **UNVERIFIED**, and the RFC's documented route is the list, not that form.
8. **Result.** IANA lists the NID in the Formal URN Namespaces table with a reference: an RFC, a template file such as `urn-formal/wmo`, or the registrant's URI ([registry](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml)).
9. **Later changes.** Revise the template and repeat the steps; describe differences from the prior version ([6.2](https://www.rfc-editor.org/rfc/rfc8141#section-6.2)).
10. **Tracking.** No tracker is documented. Practical options are the public list archive and the registry page (suggestion). The 2022 archived thread shows a requester asking about status after a period of delay ([archive](https://mailarchive.ietf.org/arch/msg/urn/9WARfIqddxTmm3Gia6xPctL36d8/)); treat that as an anecdote, not as a typical duration.

## 6. Identifier lifecycle (OGC Naming Authority statuses)

Source: [OGC Naming Authority - Procedures, 09-046r6, version 1.3, published 2021-09-27](https://docs.ogc.org/pol/09-046r6.html), clause 7.3. It is the revision listed on the [OGC glossary page](https://www.ogc.org/ogc/glossary/n) when fetched; `09-046r7` returned HTTP 404 at the same path, so I call r6 the latest I found, not confirmed current. The earlier [09-046r5 (v1.2)](https://docs.ogc.org/pol/09-046r5.html) listed only "proposed | valid | invalid | superseded | retired."

Clause 7.3 first describes the register-item flow: "Items are inserted into the relevant OGC-NA Registers on submission, with the status 'invalid'. If a registration request is accepted the item status is set to 'valid'. Items may subsequently be 'superseded' (typically if the locator is changed) and a pointer to its successor recorded, or 'retired' (if the resource is no longer available). An item that supersedes an earlier item shall have a pointer to its predecessor." It then says a proposal management record "shall be maintained with the following status flags." The list has **eleven** flags, not six. All six named in the request exist; five more are present.

**A discrepancy inside the source (not resolved here).** The prose says new items start as `invalid`, while the flag definitions define `submitted` as "entered into the register, but the control body has not accepted the proposal" and `invalid` as a previously valid item found to contain a substantial error. The text does not reconcile these. The owner should not rely on either reading without asking the OGC Naming Authority.

| Status (exact) | Definition (quoted from 09-046r6 clause 7.3) | How a URN namespace spec could express it (SUGGESTION, not from the source) |
|---|---|---|
| `deprecated` | "The resource is superseded and will become obsolete, use only for historical purposes. (Source: ISO 19115-1: 2014)" | Keep the URN assigned and resolvable; mark as discouraged in the register entry. |
| `experimental` | "Development of the resource is on-going and changes (including withdrawal) may be made without warning." | A spec using this flag would need to state that the URN itself is still never reassigned, even if the resource changes or is withdrawn ([RFC 8141 section 5](https://www.rfc-editor.org/rfc/rfc8141#section-5)). |
| `invalid` | "A decision has been made that a previously valid register item contains a substantial error and is invalid, and will normally have been replaced by a corrected item. (Source: ISO 19135-1:2015)" | Name stays reserved and never reused; entry links to its corrected replacement. |
| `notAccepted` | "The proposal is rejected. (Adapted from: ISO 19115-1: 2014)" | Proposal recorded but no URN is minted. |
| `proposed` | "It is suggested that development of the resource needs to be undertaken. (Adapted from: ISO 19115-1: 2014)" | A candidate name in the register, not yet assigned. |
| `reserved` | "This resource is reserved." | Segment or name held for future use. |
| `retired` | "A decision has been made that the item is no longer recommended for use. It has not been superseded by another item. (Source: ISO 19135-1:2015)" | URN remains valid and never reassigned; register entry shows retired. |
| `stable` | "progress concluded and no changes will be accepted (same as the 'final' status code in ISO 19115-1:2014)" | Definition is frozen for that version. |
| `submitted` | "The item has been entered into the register, but the control body has not accepted the proposal to add it. (Source: ISO 19135-1:2015)" | Entry exists pending decision by the namespace's assigning body. |
| `superseded` | "The item has been superseded by another item and is no longer recommended for use. (Source: ISO 19135-1:2015)" | Old entry carries a pointer to its successor. |
| `valid` | "The item has been accepted, is recommended for use, and has not been superseded or retired. (Source: ISO 19135-1:2015)" | Entry is assigned and recommended. |

**Pointer rule (quoted):** a superseded item has "a pointer to its successor recorded," and "An item that supersedes an earlier item shall have a pointer to its predecessor." So a superseding entry points back at its predecessor.

**How this interacts with RFC 8141.** A URN, once assigned, is "never assigned to more than one resource and never reassigned to a different resource ... even if the name itself is deprecated or becomes obsolete" ([RFC 8141 section 5](https://www.rfc-editor.org/rfc/rfc8141#section-5)). Statuses are properties of register entries, not a way to recycle names. RFC 7467 is one precedent for recording a status inside a namespace ("active" or "archive," [section 2.7](https://www.rfc-editor.org/rfc/rfc7467)). Whether the template's Assignment field may reference such a register is for the owner to decide; the RFC does not require one. Also note that the OGC document governs OGC-NA registers for `urn:ogc` and `http://www.opengis.net` names; applying its statuses to a separate NID is a design choice by the owner, not something that document requires.

## 7. How OGC handles its own NID, and "registering inside an existing authority"

OGC's formal NID `ogc` is registered through [RFC 5165](https://www.rfc-editor.org/rfc/rfc5165), with OGC as declared registrant and the OGC Naming Authority (ONA) managing assignment of the resource-type segment. Under [09-046r6](https://docs.ogc.org/pol/09-046r6.html) the form is `urn:ogc:` + resource type + `:` + a resource-specific string; types come from an OGC-NA register; a name is requested by a proposal to `names@opengeospatial.org` (clause 7.2; the form `names@ogc.org` appeared only in a search snippet and is **UNVERIFIED**); new types need a Name Type Specification and new authorities a Name Authority Proposal (clauses 6.5 and 6.7). RFC 5165 says "any individual or organization can make a contribution by submitting a proposal to the OGC for consideration by the ONA" ([section 5](https://www.rfc-editor.org/rfc/rfc5165)).

"Registering inside an existing authority" therefore means getting names assigned under a namespace someone else already holds, by that body's procedure, instead of obtaining a new NID from IANA. This is an alternative only; I did not verify whether the OGC-NA would accept names for an external standard, its eligibility rules, or timing (**UNVERIFIED**), and I make no recommendation.

## 8. Alternatives if registration is declined or delayed (facts only)

- **`urn:example` for drafts.** Registered under [RFC 6963](https://www.rfc-editor.org/rfc/rfc6963) for "documentation and in URN-related testing and experimentation." The RFC says such URNs are "NOT RECOMMENDED" for purposes other than "documentation, private testing, and truly experimental contexts," they are not meant for "building higher-level applications ... (e.g., as XML namespace names)," and uniqueness "cannot be guaranteed." Its section 5 says it does not replace registering a new NID and warns against "shadow NIDs such as `urn:example:MyCompany:*`." RFC 8141 Appendix C also points experimental usage to `example` ([RFC 8141](https://www.rfc-editor.org/rfc/rfc8141#appendix-C)).
- **Informal `urn-<number>`.** A full namespace in which IANA, not the registrant, assigns the NID, formed as `urn-` plus the next positive integer ([RFC 8141 section 5.2](https://www.rfc-editor.org/rfc/rfc8141#section-5.2)). It follows the same Expert Review policy ([IANA registry](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml)). On 2026-10-28 the highest entry listed was `urn-8`; the number a new request would receive is IANA's to assign and is not predicted here.
- **Registering inside an existing authority.** The name is assigned under a namespace that someone else already holds, using that holder's own procedure; no new IANA NID is requested. For `urn:ogc` that procedure is a proposal to the OGC Naming Authority ([09-046r6 clause 7.2](https://docs.ogc.org/pol/09-046r6.html)). Whether the OGC-NA would accept names for an external standard is **UNVERIFIED**.
- **A controlled http(s) URI.** [RFC 6963 section 1](https://www.rfc-editor.org/rfc/rfc6963) notes it "is relatively easy to mint URIs whose authority component is a domain name controlled by the person or organization." OGC's own policy compares the two: "URN NID registrations ... are forever, while http domain registration is only as long as the owner remembers," and "use of http URIs as persistent identifiers requires a reliable strategy for managing the domain, the server," as well as protection against organizational name changes ([09-046r6 clause 9](https://docs.ogc.org/pol/09-046r6.html)). Related, [RFC 4151](https://www.rfc-editor.org/rfc/rfc4151) defines the `tag:` scheme, built from a domain name or email address plus a date, for which "no central registration is necessary" and which has "no authoritative resolution mechanism."

## 9. Checklist (tick as you go; every item is the owner's action)

- [ ] Re-check the live [IANA registry](https://www.iana.org/assignments/urn-namespaces/urn-namespaces.xhtml) for `autonomyml` (last seen absent, registry dated 2026-10-28).
- [ ] Do my own trademark and name-confusion check (including the similar-looking "AutonoML" noted in section 2.2); decide whether it affects the Interoperability field.
- [ ] Decide formal NID vs informal `urn-<number>` vs `urn:example` vs another route (sections 2 and 8).
- [ ] Decide registrant (person, project or organization), address and contact; accept that these become public.
- [ ] Decide whether fast track (RFC 8141 section 6.3) is claimed and, if so, on what authorization.
- [ ] Decide the URN structure after `urn:autonomyml:` and the equivalence rules.
- [ ] Decide who assigns names, the uniqueness mechanism, and the non-reassignment commitment.
- [ ] Decide resolution intent (none, planned, or a named service).
- [ ] Write or locate a stable specification and publish it at a stable URL.
- [ ] Complete the 13 Appendix A fields with no leftover `OWNER TO DECIDE`.
- [ ] Decide whether to adopt OGC-NA register statuses and how they map (section 6); note the `submitted`/`invalid` ambiguity.
- [ ] Read the `urn@ietf.org` list rules and archive; decide whether to subscribe and post.
- [ ] Send the template to `urn@ietf.org` (not `urn-nid@...`); respond to review comments and re-send as needed.
- [ ] Confirm the IANA registry entry after approval and record the reference.

## 10. What I could not verify or access

- **Review duration.** [RFC 8141](https://www.rfc-editor.org/rfc/rfc8141) states no timeline or fee; I found no official service-level statement. Archived threads show requests taking some time but are anecdotes.
- **The `urn@ietf.org` list rules.** The Mailman 3 list page returned HTTP 403, so posting and subscription requirements are unverified. Two list-info URLs appear in archived headers (`https://www.ietf.org/mailman/listinfo/urn` in 2022; a `urn-join@ietf.org` address in 2024); which is current is unverified.
- **IANA submission route.** The IANA registry page names no form, list or contact. The generic IANA request form's use for NIDs is unverified.
- **Exact expert powers on refusal.** Not described in RFC 8141 beyond sections 6.2 and 5.1.
- **Fast-track eligibility.** No list of "recognized" standards bodies found; the decision belongs to the IESG ([6.3](https://www.rfc-editor.org/rfc/rfc8141#section-6.3)).
- **OGC-NA current revision and contact.** `09-046r7` was not found; the OGC GitHub README did not state how names are submitted or a contact; `https://www.ogc.org/standards/na` (named in that README) was not fetched; the `names@ogc.org` variant is unconfirmed.
- **RFC 3406** (obsoleted template) was not read; the old-to-new mapping in section 4 is my reading of RFC 8141 and the four RFCs.
- **Trademark and conflict clearance** for `autonomyml`: only a single web search was done.
- **Changes after 2026-10-28** to the IANA registry are not reflected.
- Parts of RFC 8141 not read in detail: section 3.2 examples, section 8 and the reference lists. The RFC texts were taken from rfc-editor.org plain-text files; IANA template files and OGC documents were taken from their HTML pages.
