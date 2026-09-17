---
name: stl-mesh-analysis
description: Analyzes STL meshes with trimesh (bounding box, volume, watertightness, defects) and writes a markdown report; falls back to summarizing reference material when no STL is present.
---

# Skill: STL Mesh Analysis

Trigger: an STL file is present in stl_pipeline/input/, or a design brief with
no STL needs a technical read-out before spec-writing.

Procedure:
1. If an STL exists in stl_pipeline/input/, run a Python script (trimesh) to
   compute: bounding box (X/Y/Z in mm), volume, surface area, triangle count,
   is_watertight, number of separate connected components, center of mass.
2. Flag obvious defects: non-manifold edges, degenerate faces, flipped
   normals, disconnected shells.
3. Write the findings to stl_pipeline/reports/analysis_<name>.md as a short
   markdown table plus a 3-5 line plain-English summary.
4. If no STL is provided, summarize the reference material (photos, text,
   sketches) into the same report format instead, marking measured fields as
   UNKNOWN where they cannot be derived.
5. Never write to stl_pipeline/input/. Read-only on the source file.