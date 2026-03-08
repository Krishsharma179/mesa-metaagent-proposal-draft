# mesa-geo-proposal-draft
Documentation and draft for my GSoC 2026 proposal: Refactoring Mesa-Geo RasterLayer to use Mesa Core's PropertyLayer architecture. Includes technical research, proposal drafts, and system design diagrams.

# Mesa-Geo GSoC 2026 Proposal: PropertyLayer Refactor

> **Applicant:** Krish Sharma  
> **Organization:** Mesa/Mesa-geo  
> **Program:** Google Summer of Code 2026  
> **Status:** 🟡 Research & Draft Phase


## Overall Project goal
Deliver a Mesa‑Geo release that is intuitive and aligned with Mesa's modern space architecture. The project will:

1.Replace per‑cell Python attributes with PropertyLayer arrays for raster storage, keeping CRS and affine metadata intact.
2.Introduce a fluent aggregation API for per‑cell operations, filtering, mapping and neighbourhood statistics on raster data.
3.Migrate GeoSpace and raster rendering to Mesa's SpaceRenderer/Solara backend to ensure compatibility with Mesa 3.3 and later.
4.Explore, as time permits, how Mesa‑Geo can plug into Mesa's upcoming multi‑space design and position/index translation hooks.


## My understanding till now 

## 🎯 Project Overview

Refactor Mesa-Geo's `RasterLayer` to use Mesa Core's `PropertyLayer` architecture.

**Goal 1:** `RasterLayer = DiscreteSpace + PropertyLayer + CRS`

**Benefits:**
-  Vectorized NumPy operations (`layer[:] = 0`) → 10-100x faster
-  Clean API (`agent.elevation` instead of `layer.get_cell(row, col)`)
-  Aligns with Mesa 4.0 space architecture (Discussion #2585:https://github.com/mesa/mesa/discussions/2585#discussioncomment-11732488)

-  Preserves GIS features (CRS, affine transform, multi-band)

## 🔑 Key Insight from Mesa Core Discussion #2585

> *"Raster layer could be discrete space with property layers + CRS"*  
> — @wang-boyu, Mesa-Geo maintainer

**What this means for my proposal:**
| Mesa Core Concept                 |           Mesa-Geo Application           |
|-----------------------------------|------------------------------------------|
| `cell.coordinate` (logical index) | `cell.rowcol` (grid row/col)             | 
| `cell.position` (physical coords) | `cell.xy` (GIS coordinates in CRS)       |
| PropertyLayer (NumPy array) | Raster bands (elevation, temperature, etc.)    |
| DiscreteSpace base class | RasterLayer inherits DiscreteSpace + GIS metadata |


I understood the property layer and discrete space architecture today
property layer:[property_layer.md](Research/property_layer.md)
discrete layer:


## Relevant links 

Refactor RasterLayer to be based on PropertyLayer in Mesa #201:
https://github.com/mesa/mesa-geo/issues/201

Cell aggregation API in raster layer : https://github.com/mesa/mesa-geo/issues/81

Add Cell.xy for RasterLayer cell coordinates and clarify pos/indices semantics:
https://github.com/mesa/mesa-geo/pull/299

GeoSpace visualization incompatible with Mesa ≥ 3.3 (SolaraViz API change):
https://github.com/mesa/mesa-geo/issues/295

Integration Proof of Concept: Prototype a GeoSpace redesign that follow https://github.com/mesa/mesa/discussions/2585#discussioncomment-11732488.


## My contributions:

Pr:fix: use weakref in EventGenerator to prevent memory leak:https://github.com/mesa/mesa/pull/3360 status=Merged

PR:fix: prevent time rewind in _advance_time by adding early return:
https://github.com/mesa/mesa/pull/3329 status=Merged

Opened Issue:Adding rasie value error in DiscreteSpace.add_cell() on duplicate coordinates:
https://github.com/mesa/mesa/issues/3469

Pr:Fix duplicate coordinate validation:
https://github.com/mesa/mesa/pull/3473 status:Open



## 💬 Get in Touch

I welcome feedback and collaboration! Feel free to:
- Open an issue in this repo for proposal questions
- Comment on Mesa-Geo discussions to coordinate efforts
- Reach out via Mesa community channels (Matrix)

---
*Last updated: March 2026*  
*This is a living document — check back for updates!*