# Skill: STL Design Specification Writing

Trigger: an analysis report exists at stl_pipeline/reports/analysis_*.md.

Procedure:
1. Read the analysis report and the original user request.
2. Write stl_pipeline/specs/spec_<name>.md with these sections:
   - Purpose (what the object is for)
   - Overall dimensions (mm, with a stated tolerance, e.g. ±0.2mm)
   - Material assumption and printer bed size
   - Minimum wall thickness / minimum feature size
   - Print orientation and whether supports are allowed
   - Max overhang angle
   - Fit / tolerance requirements for any mating parts
   - Acceptance criteria checklist (bullet list a validator can literally tick)
   - Open questions (anything genuinely ambiguous, left for the user)
3. Separate "Hard requirements (from the user)" from "Assumed defaults" in
   two clearly labeled subsections.
4. Do not include any CAD script or pseudo-code — this document is
   implementation-agnostic.