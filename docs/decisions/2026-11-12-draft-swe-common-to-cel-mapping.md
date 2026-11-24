> Checked against the pinned text on 2026-11-14; differences are listed in the decision record, section "SWE Common mapping checked against the pinned text".

# Draft: SWE Common 3.0 types to CEL types (proposals, not decisions)

Status: **draft, 2026-11-12. Not normative. All nine choices below were decided by the owner on 2026-11-12 (see the decision record); the table rows themselves are still the Architect's proposals except where a choice changed them, and the table has not been checked against the pinned SWE Common 3.0 text.** Every mapping below is the Architect's proposal. Written after the owner chose to map every SWE Common type with a defined shape (see the decision record, "Type mapping: every SWE Common type, with defined shapes") and asked for a table to review.

## Sources and their limits

- **CEL:** `google/cel-spec` tag `v0.26.0`, commit `21ec6f4e52e8d694687ff9ed7408d3eccbb955d7` (the pinned release; `doc/langdef.md`). Read directly at the pin.
- **SWE Common:** the JSON schemas under `swecommon/schemas/json/` of `opengeospatial/ogcapi-connected-systems`, clone at commit `fb858be23aa03e2b824ec50b5a97ac2c2a1d3fec` (2026-09-21). **This is not the pinned SWE Common 3.0 text (OGC 24-014).** Names and property lists must be re-read against the pinned standard before any wording. The standard's prose (`swecommon/standard/24-014.adoc`) was not read; only the schemas.
- Nothing about the project was sent to any service; both repositories were cloned read-only.

## Facts from the sources that the proposals rest on

1. **CEL's types** are `bool`, `int`, `uint`, `double`, `string`, `bytes`, `list`, `map`, `null`, `timestamp`, `duration` and `type`. CEL has no decimal type and no unit type.
2. **CEL's type check needs exact types.** "Comparisons require strict type equality at type-check time"; only at run time are `int`, `uint` and `double` compared across types. So a condition `level < 20` against a `double` field fails the start-time type check; the author must write `level < 20.0`. This follows from the decision to type-check at start and is not a design choice of this table.
3. **CEL and JSON:** a JSON number converts to `double`; the strings `"NaN"`, `"Infinity"`, `"-Infinity"` are the JSON form of the special doubles; an object converts to a `map` with string keys; an array to a `list`. Any ordering comparison with `NaN` is false, and `NaN == NaN` is false.
4. **SWE Common already defines missing values.** Every simple component has an optional `nilValues` list of reserved values, each with a `reason` (a URI) and a `value` (for example `-9999` with a reason of "missing"). A Quantity value may also be the special string `"NaN"`, `"Infinity"`, `"+Infinity"` or `"-Infinity"`. A Time value may be an ISO 8601 date-time string or a number or one of those specials. So "missing" has a schema-defined form per component, which answers part of the open per-type missing-marker question (see Choice 2).
5. **Components are structured by schema, values by block.** A `DataRecord` has a list of named `fields`, each a component; a `Vector` has `coordinates`; a `DataChoice` has `items` and a `choiceValue` (a Category) naming the chosen item; a `DataArray` and a `Matrix` have an `elementType` and an `elementCount`; a `DataStream` has an `elementType`, an `encoding` and `values`. A `Geometry` has an `srs` (a coordinate reference system) and a GeoJSON `value`.
6. **Quantity, Time and ranges carry a `uom`** (unit reference with a UCUM code or a URI). CEL has no unit; the unit stays in the schema.

## The table

"Proposed CEL type" is what a condition sees when it reads a value of that component type by field path. "No-data" is when the value counts as no observation (the decided rule). Unflagged rows are low-risk; **flagged rows need your choice** (numbers are in the next section).

| SWE Common type | Proposed CEL type | Notes and flags |
|---|---|---|
| Boolean | `bool` | none |
| Count | `int` | integer values; a nil value counts as no-data |
| Quantity | `double` | the value is always `double`, even if the JSON shows a whole number (see fact 2: authors write `20.0`); the unit stays in the schema; **no conversion** (Choice 3). `NaN` and `Infinity` appear as the special doubles; a `NaN` or a nil value counts as no-data (decided for NaN); `Infinity` is **not** no-data (Choice 2) |
| Text | `string` | a nil value counts as no-data |
| Category | `string` | the code from the dictionary named by `codeSpace`; no enumeration check by CEL (the schema `constraint` is the schema's business, **Choice 4**) |
| Time | `timestamp` | an ISO date-time string maps directly. A numeric time (seconds after an epoch given by `referenceTime`, or relative) maps only if the schema gives a `referenceTime`; otherwise the type check rejects use as `timestamp` (**Choice 5**) |
| CountRange | `list(int)` of two elements | `[min, max]` |
| QuantityRange | `list(double)` of two elements | `[min, max]`, unit in the schema |
| TimeRange | `list(timestamp)` of two elements | same numeric-time caveat as Time |
| CategoryRange | `list(string)` of two elements | ordered by the codespace's own order, which CEL cannot check; ordering by string comparison would be wrong (**Choice 6**) |
| DataRecord | `map(string, dyn)` read by field name | field names as in the schema; a field read gives the CEL type of that field's component; the type check is done per field from the schema |
| Vector | `map(string, double)`, keyed by coordinate name | each coordinate is a Quantity; `referenceFrame` stays in the schema; same as a record of Quantities |
| DataArray | `list` of the element type | whole-array reads allowed; the element count is the list size; **large arrays are a cost and limit problem** (**Choice 7**) |
| Matrix | `list(list(double))` in row-major order | a matrix is an array with a frame; the shape comes from `elementCount`; same cost limit as DataArray (Choice 7) |
| DataChoice | `map` with exactly one key, the name of the chosen item | no CEL construct exists; the proposal turns "which item is present" into `has(x.itemName)` (the CEL presence macro) so a condition can test the chosen alternative (**Choice 8**) |
| ~~DataStream~~ | *dropped 2026-11-24* | the pinned SWE Common 3.0 text says a DataStream is not a component and cannot be a result schema, so no condition can read one; the row never applies (see the decision record) |
| Geometry | `map(string, dyn)` holding the GeoJSON object (`type`, `coordinates`); **amended 2026-11-24: no `srs` entry, the `srs` stays in the schema; only the six GeoJSON types the pinned text allows** | readable but **not testable**: built-in CEL has no geometry functions (the standard's own function set is a deferred extension), so a condition can read `coordinates` as numbers and compare them, but cannot ask "inside this area". Coordinate reference system rules deferred (**Choice 9**) |

## Choices that need the owner (each would be one card)

1. **Which table rows to accept as drafted. DECIDED 2026-11-12 (the five simple rows accepted, with the CEL environment typed from the result schema so record fields are checked at start).** The unflagged rows (Boolean, Count, Text, DataRecord, Vector) can be accepted together in one decision.
2. **Missing values per type. DECIDED 2026-11-12 (NaN and declared nil values; infinities stay readable; see the decision record).** SWE Common gives each simple component a `nilValues` list. Proposal: a value counts as no-data when it equals one of the component's declared `nilValues`, or is `NaN`, or (for Time) is a special "nil" time. `Infinity` and `-Infinity` are real numbers and stay readable, so a condition can see them. An alternative is to treat infinities as no-data too. This closes the per-type missing-marker question, and extends the decided NaN rule to the schema's own markers.
3. **Units. DECIDED 2026-11-12 (declared in the specification, checked at start, no conversion; see the decision record; the proposal text below was not followed in detail).** Proposal: no conversion and no unit check; a condition compares numbers in the unit the schema declares. A start-time warning or rejection when a condition compares two values with different units is not possible, because CEL has no units. The risk is a silent unit mistake (the drivers read earlier use degrees Fahrenheit and inches of mercury). An alternative is to require that every Quantity read in a condition has a declared unit and a binding-supplied check, which the standard cannot test in plain CEL.
4. **Category constraints. DECIDED 2026-11-12 (plain text, no ordering, no start check of codes; see the decision record).** Proposal: CEL sees only the string; any allowed-token list in the schema is not enforced by CEL.
5. **Numeric time. DECIDED 2026-11-12 (timestamp when it can be one; see the decision record).** Proposal: a Time whose value is numeric is readable as `timestamp` only if the schema gives a `referenceTime`; otherwise reading it as a timestamp fails the start check. An alternative is to read it as a `double` plus unit.
6. **CategoryRange ordering. DECIDED 2026-11-12 (same decision as Choice 4).** Proposal: readable as a pair of strings, but a condition cannot rely on string order; the standard says so in a Note.
7. **Arrays, matrices and streams: size and form. DECIDED 2026-11-12 (the specification declares a maximum size per input; start rejects a larger declared count, run time treats a larger value as no observation; out-of-band values are not readable; see the decision record).** Proposal: readable as lists; the standard states a maximum size per read (not drafted; it would be a number the owner sets) and says that out-of-band or link values (`result@link`, a stream's out-of-band `values`) are not readable in a condition.
8. **DataChoice shape. DECIDED 2026-11-12 (one-key map tested with has(); see the decision record).** Proposal: a one-key map tested with `has(...)`. This is the only mapping that invents a shape. An alternative is to hand the condition only the chosen item's name as a string.
9. **Geometry. DECIDED 2026-11-12 (readable as numbers, limits stated, no reference-system check; see the decision record).** Proposal: readable as a GeoJSON map with its `srs`, with no spatial functions in the first version. The owner's "own function set" decision (deferred) is the route to spatial tests. A condition on geometry is therefore limited to comparing coordinate numbers, and the standard must say that coordinates in different reference systems are not comparable (not enforceable in CEL).

## Gaps and things not checked

- The pinned SWE Common 3.0 prose (24-014) and its requirement classes were not read; only the repository's JSON schemas. The JSON Schema `Quantity` value form `NumberOrSpecial` and the nil-value form are from those schemas.
- Whether the API's observation result for a given result schema always arrives as plain JSON values, or may arrive in the SWE Common block encodings (text, binary), was not checked beyond noting the media types. The proposal assumes the JSON form.
- How the executor obtains a result's schema type at start (the datastream's schema resource, per Part 2) was seen in outline only; the start-time type check depends on it.
- The CEL `dyn` type weakens the start-time check for record fields (a field read yields its schema type, but a map read through `dyn` is checked only at run time). Whether the standard requires a typed environment built from the schema (so record fields are checked at start) was not worked out; it is the key to making "type check at start" meaningful and should be decided with Choice 1.
- Time zone and leap-second rules for timestamps (CEL has its own rules, `langdef.md` "Timezones") were not compared with SWE Common's.
