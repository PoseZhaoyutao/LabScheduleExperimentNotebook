# 2026-06-14 Session Memory

## Role and Collaboration Context

The user wants Codex to act as a PhD research partner working alongside Claude Code. At the start of each session, Codex should check for the latest Claude Code memory or project context when available.

For this workspace, no project-specific `CLAUDE.md` or AgentMaker-specific Claude memory was found. The usable active memory came from:

- The user-provided AGENTS.md instruction.
- The existing AgentMaker repository structure.
- The current design discussion in this session.

## Product Goal

Create a local-first web app for schedule management and biological experiment recording.

The first version should focus on experiment templates and include some schedule planning. Research context is herpesvirus assembly/release, especially gamma-herpesvirus tegumentation and secondary envelopment.

## Confirmed Product Decisions

- First deliverable shape: local web app.
- Data and AI boundary: local-first with optional future AI integration.
- Home page priority: experiment record template workspace.
- Storage behavior: browser local save plus import/export.
- Main feature priority: experiment templates first, light schedule planning second.
- Research roadmap: keep lightweight in MVP.
- Personal planning: include a simple life/other To-do list.
- Long-term personal tasks can be configured to appear daily, every N days, weekly, near deadline, or after a hidden-until date.

## Confirmed Experiment Templates

MVP templates:

- qPCR.
- Immunofluorescence.
- Western blot.
- General cell experiment.

qPCR must support the user's real workflow:

- The user prepares reactions in 8-strip qPCR tubes.
- The app should allow input strip by strip.
- The app should map strip layouts into a 384-well plate.
- Mapping should support orientation changes, rotation, drag/move of target regions, technical replicates, and export of a plate map or loading table.

Transfection/cell experiment requirements:

- Common plate formats are 24-well and 6-well plates.
- Experiments often use one or two plasmids.
- The template must capture plasmid concentration, amount, calculated volume, transfection reagent brand/amount, and final transfection volume.
- The template must support optional viral infection with virus strain, MOI or inoculum, infection timing, and collection timing.

## Design Artifacts

The formal design spec is:

- `docs/superpowers/specs/2026-06-14-lab-schedule-experiment-notebook-design.md`

Temporary visual brainstorming mockups were created under `.superpowers/brainstorm/` and are intentionally ignored by git.

## Next Recommended Step

After the user reviews the design spec, create an implementation plan before writing app code. The plan should break work into:

- App scaffold and local storage.
- Record schema and repositories.
- Experiment template editors.
- qPCR strip-to-384 mapper.
- Cell/transfection plate editor.
- Schedule and To-do views.
- Import/export.
- Verification.
