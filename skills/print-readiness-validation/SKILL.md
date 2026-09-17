# Skill: Automated Print-Readiness Validation

Trigger: a new STL appears in stl_pipeline/design/output/.

Procedure:
1. Load the STL (trimesh) and run:
   - is_watertight
   - is_winding_consistent
   - Euler number sanity check
   - connected-components count (flag if >1 unless the spec calls for a
     multi-body plate)
2. Compare the bounding box against the printer bed size stated in the spec
   — flag any axis that exceeds it.
3. Approximate minimum wall thickness (ray-casting or an equivalent
   thickness-analysis pass) and compare against the spec's minimum feature
   size.
4. Sanity-check volume order of magnitude against the stated dimensions
   (catches unit/scale mistakes, e.g. a model 1000x too small or too big).
5. Write stl_pipeline/reports/validation_<name>.md: one row per check with
   PASS/FAIL, and an overall verdict line.
6. On any FAIL, list numbered, actionable fixes the DESIGNER can act on
   directly (e.g. "wall at coordinate X,Y is 0.6mm, spec requires 1.2mm
   minimum — thicken this feature").
7. Never auto-repair the mesh silently; a repair, if attempted, must be
   logged as its own explicit step, not folded into the validation report.