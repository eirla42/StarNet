---
name: visual-qa-signoff
description: Renders the validated STL from multiple angles and checks it against the spec and reference inputs to issue an APPROVED or REJECTED final QA sign-off.
---

# Skill: Visual QA & Final Sign-off

Trigger: stl_pipeline/reports/validation_<name>.md exists with an overall
PASS verdict.

Procedure:
1. Render the candidate STL from at least 4 angles (front, top, isometric,
   bottom) to PNG under stl_pipeline/renders/, e.g. via a trimesh scene
   export or `openscad --render --imgsize=1024,1024`.
2. Visually inspect each render for: missing geometry, wrong proportions
   versus the spec's stated dimensions, unintended holes, disconnected
   floating pieces, unwanted asymmetry, illegible text/engraving if any.
3. Compare against the original request and any reference image supplied by
   the user.
4. Write stl_pipeline/reports/qa_feedback_<name>.md starting with exactly
   one line: "APPROVED" or "REJECTED", followed by a numbered list of
   specific reasons if rejected.
5. This report is the line's loop gate: APPROVED routes the job to the
   OUTBOX; REJECTED routes it back to DESIGNER carrying this file as the
   fix brief.