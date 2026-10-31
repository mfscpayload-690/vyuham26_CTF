# Paper Neighbourhood

- **Category:** OSINT
- **Points:** 121
- **Status:** Solved
- **Timestamp:** October 31, 2026 &mdash; 14:03:00 IST
- **Artifacts:** `sheet_urls.json`, `sheets/` (Sanborn Fire Insurance map sheets and crops)

---

## 1. Challenge Overview

An archival geospatial OSINT investigation based on historical Sanborn Fire Insurance maps from Key West, Monroe County, Florida (Library of Congress series). The challenge prompts operators to locate a specific historical business/property, cross-referencing parcel numbers, street boundaries, and church/school landmarks.

## 2. Archival Sourcing & Cartographic Indexing

Sanborn Fire Insurance Maps document building construction materials (brick, wood, frame), heights, street addresses, and property usage during the late 19th and early 20th centuries.

The archival collection is cataloged in `sheet_urls.json`:
- **Location:** Key West, Monroe County, Florida
- **Archive:** Library of Congress (`LOC_sanborn01291_003`)
- **Sheets:** Sheets 1 through 24 + specials and title sheets

## 3. Geospatial Reconnaissance & Landmark Correlation

Key blocks investigated:
- **Block 104 & 89:** Residential and commercial strips along historic Key West thoroughfares (`block_104_full.jpg`, `block_89_full.jpg`).
- **Landmarks Identified:**
  - Zion Church (`zion_church_crop.jpg`)
  - City Public School / Colored School parcel (`city_school_sheet.jpg`, `colored_school_zoom.jpg`)
  - Commercial merchants: Sam Wolf, Menendez tobacco/cigar factory properties (`sam_wolf_exact.jpg`, `menendez_label.jpg`).

## 4. Resolution & Flag Extraction

Correlating the target parcel coordinates on Sheet 16/17 against historical census and city directory records identified the exact target establishment and address, fulfilling the flag specification.

## 5. Security & Intelligence Insights
- Historical cartographic intelligence (Sanborn, USGS, Cadastral surveys) provides high-resolution ground truth for physical infrastructure, property transitions, and archival intelligence.
