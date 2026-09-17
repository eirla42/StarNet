---
name: parametric-stl-generation
description: Creates and exports parametric CAD models from an approved design spec, iterating versions with changelog notes and confirming that a valid STL was generated.
---

# Skill: Parametric STL Generation

Trigger: an approved spec exists at stl_pipeline/specs/spec_*.md, or a
qa_feedback_*.md marked REJECTED exists for this job.

Procedure:
1. Read the spec (and, on a retry, the latest qa_feedback_*.md and
   validation_*.md for concrete fixes required).
2. Write a parametric script under stl_pipeline/design/ (prefer OpenSCAD for
   simple solids; prefer CadQuery/build123d for boolean operations, fillets,
   or complex assemblies).
3. Execute it via the terminal to export an STL into
   stl_pipeline/design/output/, e.g.:
     openscad -o design_<name>_v<N>.stl model_<name>.scad
   or run the CadQuery/build123d python script directly.
4. Increment <N> on every pass — never overwrite a previous version.
5. Append a one-paragraph changelog to the script's header comment: what
   parameters were set and, on a retry, exactly what was changed and why.
6. Confirm the export succeeded (non-zero file size, no CLI error) before
   ending the run.