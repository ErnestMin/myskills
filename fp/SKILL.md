---
name: korea-fp-guide-validation
description: Validate Function Point (FP) workbooks and function lists against the Republic of Korea SW project cost estimation guide. Use when Codex is asked to inspect FP산정, FP산정(간이법), SW개발비, SW유지관리비, or SW재개발비 Excel workbooks, check Korea guide complexity/weight/cost consistency, review ILF/EIF/EI/EO/EQ rows, produce FP validation reports, or assess submitted FP lists for audit readiness.
---

# Korea FP Guide Validation

## Purpose

Use this skill to validate FP function lists and Korea SW사업 대가산정 workbook sheets. Treat the official Korea guide and official workbook formulas as the payable-cost authority, then use independent recalculation to find inconsistencies and review risks.

## Workflow

1. Preserve the source workbook. Never overwrite user-provided `.xlsm`/`.xlsx` files.
2. Identify the workbook type and method:
   - `FP산정(간이법)`: simplified FP.
   - `FP산정`: traditional FP unless the headers clearly indicate otherwise.
   - `SW개발비 산정`, `SW개발비산정`, `SW유지관리비`, `SW재개발비 산정`: cost-summary sheets.
3. Read `references/korea-fp-rules.md` when checking guide constants, traditional complexity matrices, redevelopment fields, or cost factors.
4. For `.xlsx` report creation, use the Spreadsheets skill if available. Avoid Excel Table objects if prior Excel recovery errors are a concern; use normal ranges with filters instead.
5. Run `scripts/validate_fp_workbook.py` when a deterministic workbook scan is useful, then inspect and adapt its output to the user request.
6. Produce an auditable report containing summary, row-level findings, recalculated values, source row numbers, assumptions, and unresolved review items.

## Validation Scope

Always check:

- required hierarchy fields: application, detailed work, unit process, FP type
- valid FP type: `ILF`, `EIF`, `EI`, `EO`, `EQ`
- required count fields: `RET` for ILF/EIF, `FTR` for EI/EO/EQ, and `DET`
- traditional complexity from the guide matrix
- traditional weight from FP type and complexity
- simplified weight from Korea simplified weights
- duplicate or near-duplicate unit processes within the same hierarchy
- FP sheet totals against cost-summary sheet totals
- annual unit price and correction/profit/VAT assumptions when present

Review but do not automatically change payable FP counts for:

- EIF externality: EIF must be maintained by another application/system and only referenced by this system
- ILF independence: history, log, backup, temporary, attachment, interface, and code-like tables may be subordinate or non-business data
- repeated CRUD/service-derived candidates that may describe one elementary process multiple times
- source-code evidence that suggests missing FP functions

## Output Pattern

For workbook reviews, create outputs under the active project, usually:

```text
output/reports/<review-name>/
  <review-name>_report.xlsx
  <review-name>_report.md
  <review-name>_report.json
```

Recommended sheets:

- `요약`: source, reviewed timestamp, row count, FP totals, finding counts
- `점검결과`: finding severity/category/source row/submitted/expected/reason/recommendation
- `FP행별점검`: row-by-row original values and recalculated values
- `유형별집계`: ILF/EIF/EI/EO/EQ function count and FP totals
- `비데이터행`: skipped section/blank/header-like rows
- `검토기준`: rules, assumptions, and limitations

Use Korean in review reasons and recommendations when the user is Korean. Keep internal code identifiers and comments English-first when creating reusable code.

## Practical Notes

- macOS filenames may be NFD. Normalize display text to NFC before writing Korean filenames into reports.
- OpenPyXL may read macro formula cells as cached values only. For traditional `.xlsm`, independently recalculate `FPR`/`FPV` rather than trusting macro availability.
- In traditional workbooks, average complexity is often displayed as `A` in Korean templates, not `M`.
- Do not silently drop rows with blank FP type or missing unit process; classify them as review-required or non-data rows with source row numbers.
- If the workbook is a one-off conversion or analysis artifact, keep one-off scripts under `output/...` rather than modifying the product package.
