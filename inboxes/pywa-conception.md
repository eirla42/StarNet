Produce print-ready STL(s) for project pywa-conception: I want to make a Pywa.

A Pywa is a non-gendered fictional character, belonging to several natural elements (fire, water, nature, etc.) and having characteristics of their element (example: for nature, there is a Pywa with 2 leaves on the head).

I would like you to create the same character with other characteristics on his head and other elements:
- Nature: mushroom
- Fire: volcano
- Water: watering can

You can propose new elements and new characteristics.

However, I only want to keep the existing poses in the folder with the example STLs. Printer bed: 250x250x250 mm, material: PLA. reference_stl is C:\Projets\IA\StarNet_Folder\stl_pipeline\input — if it is a single STL, consult the stl-mesh-analysis skill to analyze and fix it; if it is a folder of STLs, consult the same skill to extract a style profile (scale, proportions, base type, level of detail) and design new pieces that match it. If no STL reference exists, design from the brief and any reference_images (), marking measured fields UNKNOWN where they cannot be derived. Always write the analysis (or style analysis) report as stl_pipeline/reports/analysis_pywa-conception.md regardless of which mode was used, so downstream steps and acceptance checks find it at the same path. Write the spec, analysis, validation and a QA feedback note that only states APPROVED once the design genuinely passes review, plus render preview PNGs. Follow stl_pipeline/ naming conventions exactly for every output file.

Procedure (follow in this order; do not skip or reorder steps):
1. Resolve reference_stl: single file, folder, or absent.
2. Single file -> run stl-mesh-analysis on it and write stl_pipeline/reports/analysis_pywa-conception.md.
3. Folder -> run stl-mesh-analysis across the set (sampled at 25 max), extract the STYLE PROFILE, and write it to the same stl_pipeline/reports/analysis_pywa-conception.md path.
4. Neither -> summarize reference_images/brief into the same report format, marking UNKNOWN fields.
5. Write stl_pipeline/specs/spec_pywa-conception.md from the brief and the analysis/style profile.
6. Design or fix the model(s); export stl_pipeline/design/output/design_pywa-conception_v1.stl.
7. Validate the model(s) against printer_bed_mm and material; write stl_pipeline/reports/validation_pywa-conception.md.
8. Render preview PNGs into stl_pipeline/renders/.
9. QA review the finished design(s) against the style profile when one exists; write stl_pipeline/reports/qa_feedback_pywa-conception.md and only write APPROVED once it genuinely passes.

Acceptance (the host checks these when you finish — the task is not done until every one holds):
- print-ready STL exists
- spec written
- analysis or style report written
- validation report written
- QA approved
