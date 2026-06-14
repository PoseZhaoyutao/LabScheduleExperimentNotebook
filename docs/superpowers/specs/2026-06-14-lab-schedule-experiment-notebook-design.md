# Lab Schedule and Experiment Notebook App Design

## Product Outcome

Build a local-first web app for daily biological experiment recording and planning. The first version is an experiment-template workspace with lightweight schedule planning. It is designed for herpesvirus assembly and release research, especially gamma-herpesvirus tegumentation and secondary envelopment, but the templates should remain general enough for nearby cell biology workflows.

The app should let the user quickly create structured experiment records, save them locally in the browser, export/import JSON record packages, export Markdown experiment notes, and provide clean data to an optional AI assistant in a future version.

## Confirmed Direction

- Primary deliverable: local web app.
- Design priority: experiment recording templates first, schedule planning second, research roadmap only as lightweight metadata.
- Data boundary: local-first persistence with import/export; AI is optional and not required for MVP.
- First screen: experiment template workspace.
- Storage: browser local save plus JSON/Markdown import/export.
- Non-experiment planning: include a simple personal/other To-do area with conventional tasks and long-term items that can be configured to appear daily or at a chosen display interval.

## MVP Scope

### In Scope

- A local web app that opens directly into the experiment workspace.
- Experiment templates for:
  - qPCR with 8-strip tube input mapped into a 384-well plate.
  - Immunofluorescence.
  - Western blot.
  - General cell experiments, including transfection and optional viral infection.
- Local record library with search/filter basics.
- Browser local persistence.
- JSON import/export for structured record packages.
- Markdown export for human-readable experiment notes.
- Today/week/month/quarter/year planning linked to experiment records.
- Simple life/other To-do list with long-term task display rules.
- Lightweight research-context fields for gamma-herpesvirus assembly/release work.
- AI-ready data structure for future summaries, literature/material uploads, thesis support, and next-experiment suggestions.

### Out of Scope for MVP

- Accounts, login, cloud sync, and multi-user collaboration.
- Required AI API integration.
- Full ELN/LIMS audit trails, permissions, inventory, or compliance workflows.
- Automatic literature search and autonomous scientific decision-making.
- Complex research knowledge graph. The MVP keeps project and hypothesis links lightweight.

## User Workflow

### Home Workspace

The home page uses three regions:

- Left navigation: experiment templates, record library, week/month plan, quarter/year plan, materials and AI readiness.
- Main workspace: quick creation cards for qPCR, immunofluorescence, western blot, and general cell experiments. Below that are recent records and lightweight research links.
- Right action panel: today and week actions, overdue record completion, pending review, monthly targets, quarter/year milestones, and personal/other To-do.

The default user path is:

1. Open the app.
2. Pick an experiment template.
3. Fill structured fields and execution notes.
4. Link the record to a schedule item, hypothesis, or next action.
5. Save locally.
6. Export JSON or Markdown when needed.

## Experiment Templates

### Shared Record Fields

Every experiment record has four layers:

- Basic information: title, date, experiment type, operator, project, status, tags.
- Experimental design: sample, condition, virus, cell line, plasmid, antibody, primer/probe, replicate count, plate or well layout.
- Execution record: actual recipe, volumes, timeline, instrument, reagent lot or brand, abnormal events, raw data or image references.
- Review output: result summary, whether the result supports the hypothesis, likely failure reason, next action, linked schedule item.

Shared statuses:

- Planned
- Running
- Needs data
- Needs review
- Completed
- Failed or repeat needed

### qPCR Template

The qPCR template must match the real bench workflow:

1. The user enters reactions by 8-strip qPCR tube rows.
2. Each strip contains eight positions with sample, primer/probe, condition, template, mix, replicate group, and notes.
3. The user can copy a strip, duplicate a row pattern, and batch-fill sample-first or primer-first layouts.
4. The user maps one or more strips into a 384-well plate.
5. Mapping supports horizontal fill, vertical fill, 90-degree rotation, target-region drag/move, and technical replicate expansion.
6. The app generates a complete 384-well plate map and pipetting/loading table.

qPCR fields:

- Plate-level information: date, project, operator, instrument, plate ID, kit, cycling program, detection chemistry.
- Strip-level information: strip ID, strip order, sample order, primer/probe order, mix information.
- Well-level information: 384-well coordinate, source strip position, sample, primer/probe, condition, replicate, Ct/Cq, excluded flag, exclusion reason.
- Analysis information: reference gene, target gene, delta Ct, delta delta Ct, control condition, fold-change, notes, conclusion.

Validation rules:

- Warn if technical replicate counts are incomplete.
- Warn if NTC wells are missing.
- Warn if reference gene pairing is incomplete.
- Warn about empty wells inside a mapped block.
- Preserve both the strip input layout and the final 384-well layout in exported data.

### Immunofluorescence Template

Fields:

- Cell line, passage or condition note, seeding density, plate or coverslip format.
- Virus strain, infection status, MOI or inoculum, infection time, treatment condition.
- Fixation, permeabilization, blocking, wash conditions.
- Primary antibody: target, host, clone or catalog, dilution, incubation time.
- Secondary antibody: fluorophore, host reactivity, dilution, incubation time.
- Counterstain and mounting medium.
- Microscope, objective, channels, exposure, acquisition settings.
- Image file references, quantification method, result summary, representative image notes.
- Follow-up action and linked schedule item.

### Western Blot Template

Fields:

- Sample source, cell or virus condition, harvest time, lysis buffer, inhibitor use.
- Protein quantification method and concentration.
- Loading amount, sample buffer, denaturation condition.
- Gel percentage, running condition, transfer method, membrane type.
- Blocking condition.
- Primary and secondary antibodies with target, brand/catalog, dilution, incubation time.
- Exposure system, exposure time, image file references.
- Band quantification, normalization target, result summary.
- Abnormal events, repeat decision, follow-up action.

### General Cell Experiment Template

This template covers routine cell culture, plating, transfection, infection, treatment, and collection plans.

Plate formats:

- 24-well plate.
- 6-well plate.

Core fields:

- Cell line, passage, confluence, seeding density, medium, antibiotics, plate format.
- Well layout with per-well condition labels.
- Treatment timeline and sample collection timeline.

Transfection module:

- Supports one or two plasmids per well.
- Plasmid name, concentration, target amount per well, calculated volume, ratio, vector top-up.
- Transfection reagent brand/model, reagent amount, dilution medium, final complex volume, incubation time.
- Per-well recipe table and optional master-mix calculation.

Viral infection module:

- Infection yes/no per condition or well.
- Virus strain, stock identifier, MOI or inoculum amount, adsorption time, medium replacement, harvest time points.
- Link to downstream qPCR, IF, or WB records.

Validation rules:

- Warn when plasmid volume exceeds practical reaction volume.
- Warn when total plasmid mass does not match the target amount.
- Warn when virus infection fields are partially filled.
- Preserve plate format and well-level recipe in exported data.

## Schedule Planning

Experiment planning should be action-based rather than a standalone calendar clone.

### Experiment Schedule Views

- Today: experiments to run, records to complete, data to import, records to review.
- Week: planned experiments, repeated experiments, deadline-adjacent actions.
- Month: research target or small milestone, such as validating whether a tegument protein affects secondary envelopment-related phenotypes.
- Quarter/year: paper figures, thesis milestones, key hypothesis chain, major deadlines.

Schedule items can link to experiment records and can create follow-up prompts such as:

- Transfection at 24 hours: infect or collect sample.
- qPCR run complete: import Ct and review.
- IF imaging complete: attach representative images and quantify.
- WB exposure complete: quantify bands and decide whether to repeat.

### Life and Other To-do

The app includes a lightweight non-experiment To-do area.

Task fields:

- Title.
- Notes.
- Category: life, admin, reading, writing, other.
- Status: open, done, hidden, archived.
- Priority.
- Due date.
- Optional long-term display rule.

Long-term display rules:

- Always show daily.
- Show every N days.
- Show weekly on selected weekdays.
- Show when due date is within N days.
- Hide until a selected date.

This area should stay simple and should not compete with the experiment workspace.

## Data Model

The MVP should use IndexedDB for records and layouts because qPCR plate maps and exported record packages can become too large for reliable localStorage use. localStorage may be used only for small UI preferences such as the last opened view. The implementation should use a repository layer so storage can move to a file-backed or database-backed system in a future version.

Primary entities:

- `ExperimentRecord`
- `ExperimentTemplate`
- `PlateLayout`
- `StripLayout`
- `ScheduleItem`
- `TodoItem`
- `ResearchContext`
- `ExportPackage`

Important relationships:

- An `ExperimentRecord` may link to zero or more `ScheduleItem` objects.
- A qPCR `ExperimentRecord` owns both a `StripLayout` and a mapped `PlateLayout`.
- A transfection/cell `ExperimentRecord` owns a plate-format-specific well layout.
- A `ScheduleItem` may create or reference an `ExperimentRecord`.
- A `TodoItem` is separate from experiment records but can appear in today/week views.
- A `ResearchContext` can be attached to records and schedule items.

Export requirements:

- JSON export must preserve structured fields, layouts, schedule links, review notes, and research context.
- Markdown export should be readable as a lab note with sections for design, execution, results, review, and next actions.
- Import should validate schema version and show a recoverable error if data is incompatible.

## Implementation Units and Interfaces

The app should be split into units with clear boundaries:

- `TemplateRegistry`: defines available experiment templates, their default fields, validation rules, and export labels.
- `RecordRepository`: saves, loads, updates, deletes, imports, and exports records through IndexedDB.
- `ScheduleRepository`: stores schedule items and long-term To-do display rules.
- `QpcrStripEditor`: manages 8-strip input rows and strip-level batch operations.
- `QpcrPlateMapper`: maps strip layouts to 384-well coordinates and reports conflicts or incomplete replicates.
- `CellPlateEditor`: manages 24-well and 6-well layouts for transfection and infection records.
- `ExportService`: converts records and record packages to JSON and Markdown.
- `TodayPanel`: combines experiment actions, follow-up prompts, and personal/other To-do items that should appear today.

Interfaces between units:

- Editors produce draft record objects but do not persist directly.
- Repositories persist complete records and return schema-versioned objects.
- Validation runs before save and export, returning warnings and blocking errors separately.
- Export accepts repository objects and should not depend on UI state.
- Today/week/month views read schedule and record summaries rather than full editor state.

## AI Boundary

AI is optional in the MVP. The first version prepares for AI by exporting structured, clean records.

Future AI assistant capabilities:

- Periodically summarize experiments and schedule state.
- Read user-uploaded materials, papers, thesis drafts, and exported record packages.
- Identify missing controls, unresolved results, repeated failures, and likely next experiments.
- Suggest next experimental plans in the context of gamma-herpesvirus tegumentation, secondary envelopment, assembly, and release.

MVP must not require internet access or an API key to perform core recording and planning.

## Interface Components

- Home workspace.
- Template picker.
- Record editor.
- qPCR strip editor.
- qPCR 384-well mapper.
- Plate layout editor for 24-well and 6-well cell experiments.
- Record library.
- Today/week action panel.
- Month/quarter/year planning views.
- Simple To-do panel.
- Import/export panel.
- AI readiness panel.

## Error Handling and Edge Cases

- Local storage unavailable: show a clear warning and allow export of current unsaved data if possible.
- Import schema mismatch: show version and rejected fields instead of silently dropping data.
- qPCR mapping conflict: highlight overlapping target wells and block save until resolved.
- Incomplete qPCR replicates: warn but allow draft save.
- Missing required transfection fields: allow draft save but mark the recipe incomplete.
- Large record library: keep filters and rendering responsive; avoid loading unnecessary detail into the main list.
- Broken image/raw-data file links: preserve the text path and show that the file is not currently accessible.

## Verification Plan

MVP verification should include:

- Create and save one qPCR record from 8-strip input to 384-well mapping.
- Export qPCR record to JSON and Markdown.
- Re-import the JSON record package and verify the strip layout and plate layout are preserved.
- Create one 24-well transfection record with two plasmids and optional viral infection.
- Create one 6-well transfection record.
- Create IF and WB records with required fields and result summaries.
- Create today/week/month/quarter/year schedule entries and link at least one to an experiment record.
- Create a life/other long-term To-do item that appears daily.
- Confirm the app remains usable without AI configuration.

## Success Criteria

The design is successful when the user can:

- Use the app as a daily experiment recording workspace.
- Record qPCR according to the real workflow of 8-strip qPCR tubes mapped into a 384-well plate.
- Record transfection experiments in 24-well and 6-well formats with one or two plasmids and optional viral infection.
- Record IF, WB, and routine cell experiment details without relying on free-text notes alone.
- Link experiments to near-term and long-term schedule planning.
- Track simple life/other tasks without turning the app into a complex personal productivity system.
- Export records in formats that are useful for backup, AI review, and manuscript or thesis preparation.
