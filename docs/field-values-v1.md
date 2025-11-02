# Asset Atlas — Allowed Values (v1.3)
*File:* `/docs/field-values-v1.md`  
*Purpose:* Define standardized, limited value sets for key dropdown fields used across the Asset Atlas.  
*Scope:* Category, Owner, and License fields only.  
*Effective Date:* 2025-11-02  
*Maintainer:* Kaosisochi Unini  

---

## 1. Category
**Purpose:** Identify the primary type of asset.

| Allowed Value | Description |
|---|---|
| **art** | 2D or 3D visual assets such as sprites, tiles, or textures. |
| **audio** | Sound effects, loops, or background music. |
| **ui** | Interface elements, icons, and HUD components. |

*Rule:* lowercase, singular, concise.  
*Covers:* 100 % of current data.

---

## 2. Owner
**Purpose:** Record who created or maintains the asset.

| Allowed Value | Description |
|---|---|
| **Kenney** | Kenney.nl public asset packs (CC0 license). |
| **Kaosisochi Unini** | Original or modified internal assets. |
| **OpenGameArt** | Community-sourced assets from OpenGameArt.org. |
| **Custom / Internal** | Locally authored or studio-specific assets. |

*Rule:* capitalize proper names; consistent spacing around slashes.

---

## 3. License
**Purpose:** Define legal reuse conditions and compliance boundaries.

| Allowed Value | Conditions |
|---|---|
| **CC0** | Public domain; free for any use, no attribution required. |
| **CC BY 4.0** | Attribution required; commercial use allowed. |
| **Proprietary** | Restricted; internal or paid license required. |
| **Needs Review** | License unclear or pending validation; do not distribute externally. |

*Rule:* write license identifiers exactly as published (e.g., “CC BY 4.0”).  
*Validation:* each entry must include a `source_url` in the log for traceability.

---

### Change Log
| Version | Date | Summary | Author |
|---|---|---|---|
| v1.3 | 2025-11-02 | Limited vocabulary set to Category, Owner, and License for core metadata fields. | KU |

