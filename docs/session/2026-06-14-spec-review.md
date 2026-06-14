# 2026-06-14 Spec Review

## Review Target

`docs/superpowers/specs/2026-06-14-lab-schedule-experiment-notebook-design.md`

## Review Method

The brainstorming workflow called for a spec-document-reviewer subagent. The available subagent tool in this environment only permits spawning agents when the user explicitly asks for subagents or parallel agents, so the review was performed locally using the same checklist:

- Completeness.
- Coverage.
- Consistency.
- Clarity.
- YAGNI.
- Scope.
- Architecture and implementation boundaries.

## Findings and Fixes

### Finding 1: Storage Choice Was Ambiguous

The first draft allowed either localStorage or IndexedDB for MVP persistence. This would make implementation planning weaker because qPCR plate maps and record packages can become larger and more structured than localStorage is comfortable handling.

Fix:

- The spec now requires IndexedDB for records and layouts.
- localStorage is limited to small UI preferences.
- The repository layer remains required so storage can change later.

### Finding 2: Implementation Boundaries Needed More Detail

The first draft listed interface components but did not define implementation units clearly enough for planning and testing.

Fix:

- Added an `Implementation Units and Interfaces` section.
- Defined units such as `TemplateRegistry`, `RecordRepository`, `ScheduleRepository`, `QpcrStripEditor`, `QpcrPlateMapper`, `CellPlateEditor`, `ExportService`, and `TodayPanel`.
- Clarified that editors produce draft records, repositories persist schema-versioned records, validation separates warnings from blocking errors, export should not depend on UI state, and planning views should read summaries rather than editor state.

## Final Review Verdict

Status: Approved for user review and implementation planning.

Residual risks:

- The exact frontend stack is not chosen yet.
- The exact JSON schema should be finalized in the implementation plan.
- The qPCR mapper needs careful interaction and data tests because it is the highest-risk MVP feature.
