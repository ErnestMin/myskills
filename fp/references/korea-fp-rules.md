# Korea FP Guide Rules Reference

## Function Types

| Type | Meaning | Count Driver |
|---|---|---|
| ILF | Internal Logical File | RET x DET |
| EIF | External Interface File | RET x DET |
| EI | External Input | FTR x DET |
| EO | External Output | FTR x DET |
| EQ | External Inquiry | FTR x DET |

## Simplified FP Weights

| Type | Weight |
|---|---:|
| ILF | 7.5 |
| EIF | 5.4 |
| EI | 4.0 |
| EO | 5.2 |
| EQ | 3.9 |

## Traditional Complexity Matrices

Complexity labels in official Korean templates are commonly `L`, `A`, `H` for low, average, high.

### ILF/EIF: RET x DET

DET bands: `1-19`, `20-50`, `51+`.
RET bands: `1`, `2-5`, `6+`.

| RET \ DET | 1-19 | 20-50 | 51+ |
|---|---|---|---|
| 1 | L | L | A |
| 2-5 | L | A | H |
| 6+ | A | H | H |

### EI: FTR x DET

DET bands: `1-4`, `5-15`, `16+`.
FTR bands: `0-1`, `2`, `3+`.

| FTR \ DET | 1-4 | 5-15 | 16+ |
|---|---|---|---|
| 0-1 | L | L | A |
| 2 | L | A | H |
| 3+ | A | H | H |

### EO: FTR x DET

DET bands: `1-5`, `6-19`, `20+`.
FTR bands: `0-1`, `2-3`, `4+`.

| FTR \ DET | 1-5 | 6-19 | 20+ |
|---|---|---|---|
| 0-1 | L | L | A |
| 2-3 | L | A | H |
| 4+ | A | H | H |

### EQ: FTR x DET

DET bands: `1-5`, `6-19`, `20+`.
FTR bands: `1`, `2-3`, `4+`.

| FTR \ DET | 1-5 | 6-19 | 20+ |
|---|---|---|---|
| 1 | L | L | A |
| 2-3 | L | A | H |
| 4+ | A | H | H |

## Traditional Weights

| Type | L | A | H |
|---|---:|---:|---:|
| ILF | 7 | 10 | 15 |
| EIF | 5 | 7 | 10 |
| EI | 3 | 4 | 6 |
| EO | 4 | 5 | 7 |
| EQ | 3 | 4 | 6 |

## Cost Constants and Checks

- 2025 FP unit price: `605,784`.
- Full lifecycle stage weight default: `1.00` when template does not expose phase weighting.
- Stage split reference: analysis `0.19`, design `0.24`, implementation `0.32`, test `0.25`.
- Profit rate should not exceed the applicable guide/legal cap; previously this project used `25%` as a hard validation boundary.
- VAT is normally applied after cost plus profit and direct expenses when the workbook models VAT.

## Correction Factors

Use workbook-visible selected levels where available. Known factor scale:

| Factor | Level 1 | Level 2 | Level 3 | Level 4 | Level 5 |
|---|---:|---:|---:|---:|---:|
| Integration complexity | 0.88 | 0.94 | 1.00 | 1.06 | 1.12 |
| Performance requirement | 0.91 | 0.95 | 1.00 | 1.05 | 1.09 |
| Multi-site/operating compatibility | 0.94 | 1.00 | 1.06 | 1.13 | 1.19 |
| Security requirement | 0.97 | 1.00 | 1.03 | 1.06 | 1.10 |

## Redevelopment Review

When validating redevelopment templates, preserve and check:

- new FP
- reused-unmodified FP
- reused-modified FP
- FTR change amount/rate
- DET change amount/rate
- function change rate
- impact factor
- reuse difficulty, typically derived from structured/application clarity and documentation/source description scores
- redevelopment FP formula and workbook totals

Do not infer payable redevelopment classification solely from source code. Use source code as evidence and mark uncertain items for review.

## Common Findings

Classify findings as:

- `ERROR`: arithmetic mismatch, invalid FP type, missing required count, complexity/weight mismatch, cost total inconsistency
- `WARNING`: duplicate candidate, hierarchy issue, missing evidence, source-derived candidate not reconciled
- `INFO`: EIF externality review, low-confidence ILF pattern, assumption note, macro/cache limitation
