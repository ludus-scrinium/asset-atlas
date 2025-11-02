# Asset Atlas — Controlled Vocabularies (v1)
*File:* `/docs/field-values-v1.md`  
*Purpose:* Define standardized, limited value sets (“controlled vocabularies”) for structured metadata fields used across the Asset Atlas.  
*Source:* Derived from initial `asset-sources.csv` (Desert Shooter Pack).  
*Effective Date:* 2025-10-31  
*Maintainer:* Kaosisochi Unini  

---

## 1. Category (Primary Asset Type)

| Allowed Value | Description | Example Asset |
|----------------|-------------|----------------|
| **art** | 2D or 3D visual assets (sprites, textures, tiles). | `ART_001` – Enemy – Cactus – Front |
| **audio** | Sound effects, music loops, or voice clips. | `AUD_004` – Chime – Mono – High |
| **ui** | Interface graphics, icons, or HUD elements. | `UI_013` – Panel (Red) – Corner (L) – Square |

*Rule:* all lowercase, singular form.

---

## 2. License (Usage Rights)

| Allowed Value | Conditions | Notes |
|----------------|-------------|-------|
| **CC0** | Public domain; no attribution required. | Default for Kenney assets. |
| **CC BY 4.0** | Attribution required; commercial use allowed. | Use standard credit line. |
| **Proprietary** | Internal or restricted assets. | Use only with written consent. |
| **Needs Review** | License uncertain; pending verification. | Do not publish externally. |

---

## 3. Tech Format

| Allowed Value | Description | Typical Use |
|----------------|-------------|--------------|
| **png** | Raster image with transparency support. | Art/UI sprites |
| **ogg** | Compressed audio format. | SFX / music loops |
| **wav** | Uncompressed audio. | High-quality masters |
| **psd** | Layered source file (Photoshop). | Editable visual assets |
| **svg** | Vector graphic. | UI icons / scalable elements |

---

## 4. Display Name Structure

**Pattern**
[CategoryTerm] – [Descriptor] – [Qualifier]


| Example | Meaning |
|---|---|
| Enemy – Cactus – Front | Enemy sprite, cactus type, front view |
| Chime – Mono – High | Audio clip, mono channel, high pitch |
| Panel (Red) – Corner (L) – Square | UI panel, red theme, left corner, square shape |

*Rules*  
- Use en-dashes (–) to separate main segments.  
- Capitalize the first letter of each term.  
- Keep ≤ 50 characters total.

---

## 5. Source Name

| Allowed Value | Description |
|---|---|
| **Kenney** | Kenney.nl game-asset packs (CC0). |
| **OpenGameArt** | OpenGameArt.org community submissions. |
| **Custom / Internal** | Original or modified derivatives. |

---

## 6. Validated By

| Allowed Value | Description |
|---|---|
| **KU** | Kaosisochi Unini |
| **Unassigned** | Pending review |

---

## 7. Status (Optional Governance Field)

| Allowed Value | Description |
|---|---|
| **Draft** | Newly added; not yet validated. |
| **Approved** | Validated and ready for reuse. |
| **Deprecated** | Superseded or replaced. |

---

## 8. Field Normalization Rules

- **Dates:** ISO 8601 (`YYYY-MM-DD`)  
- **Filenames:** Uppercase prefix + sequential ID + lowercase extension (`ART_001.png`)  
- **URLs:** Full absolute path beginning with `https://`  
- **Units:**  
  - Image size → `WxH px`  
  - Audio → `SampleRate kHz / BitDepth / Channels / Duration s`

---

## 9. Accessibility & UX Guidelines

- Labels written in plain English (≤ 2 words).  
- Values legible at ≥ 12 pt, high contrast (≥ 4.5:1).  
- Dropdowns limited to ≤ 7 options per field to reduce cognitive load.  
- Tooltips or inline help for **License** and **Status** when implemented in Airtable or SharePoint.

---

### Change Log

| Version | Date | Summary | Author |
|---|---|---|---|
| v1 | 2025-11-02 | Initial vocabularies established from Desert Shooter Pack sample set. | KU |
