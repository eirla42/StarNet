---
name: stl-mesh-analysis
description: Analyzes STL meshes with trimesh — a single file or a whole folder of style-reference STLs — computing geometry stats, flagging defects, and (for folders) extracting shared style traits (scale, proportions, base type). Writes markdown reports. Falls back to summarizing reference material when no STL is present.
---

# Skill: STL Mesh Analysis

Trigger:
- A single STL file is present in stl_pipeline/input/, or
- A folder of STL files is supplied as a style reference (e.g. designing new characters that
  should match an existing set), or
- A design brief with no STL needs a technical read-out before spec-writing.

## Procedure — single reference file

1. If one STL exists in stl_pipeline/input/, run a Python script (trimesh) to compute:
   bounding box (X/Y/Z in mm), volume, surface area, triangle count, is_watertight, number of
   separate connected components, center of mass.
2. Flag obvious defects: non-manifold edges, degenerate faces, flipped normals, disconnected
   shells.
3. Write the findings to stl_pipeline/reports/analysis_<name>.md as a short markdown table plus
   a 3-5 line plain-English summary.

## Procedure — reference folder (style analysis)

4. If a folder of STLs is given as a style reference, run the same per-file trimesh pass (step 1
   metrics + step 2 defect flags) on every STL inside it. If a file fails to load, list it under
   a "SKIPPED" line with the reason — never drop it silently.
5. Cap a single batch at 25 files. If the folder holds more, sample evenly across the set,
   note the sampling method and the total file count in the report, and do not silently
   truncate.
6. Aggregate the per-file stats into a **STYLE PROFILE**: typical bounding-box range, average
   scale/height, common base/pedestal presence and rough footprint, watertightness rate across
   the set, and any defect pattern that recurs in more than one file.
7. Write stl_pipeline/reports/analysis_<name>.md — same filename convention as the single-file
   case, using whatever <name> the calling task supplies (a project name, not the folder name),
   so downstream steps and any recipe acceptance check can find it at a predictable path.
   Structure: a per-file table (same columns as the single-file table), then the STYLE PROFILE
   section, then a 3-5 line plain-English summary of what new designs should match.

## Procedure — no STL available

8. If no STL is provided at all, summarize the reference material (photos, text, sketches)
   into the single-file report format instead, marking measured fields as UNKNOWN where they
   cannot be derived.

## Rules

9. Never write to stl_pipeline/input/ or to the reference folder. Read-only on every source
   file, in both the single-file and folder cases.