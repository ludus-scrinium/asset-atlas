# Asset Atlas — File Naming Rules (v1)
**File:** `/docs/file-naming-rules.md`  
**Scope:** all asset files (art, audio, UI, docs)  
**Maintainer:** Kaosisochi Unini  
**Effective:** 2025-11-02

---

## TL;DR (Use this pattern)
[TYPE]_[Descriptor_Words]_v[Version].[ext]

**Examples**

ART_Enemy_Cactus_Front_v1.png

AUD_Loop_Forest_v2.ogg

UI_Panel_Red_CornerL_v1.png


---

## Structure (what each part means)
- **TYPE** → asset group. Use **ART**, **AUD**, **UI** (UPPERCASE).
- **Descriptor_Words** → short plain words. **Title_Case**, separated by **underscores**.
- **Version** → start at **v1**; bump to **v2, v3…** when content changes.
- **ext** → file extension in **lowercase**: `png`, `ogg`, `wav`, `psd`, `json`.

---

## Do / Don’t (at a glance)
**Do**
- Use **underscores** (no spaces).
- Keep total length **≤ 30 chars** before the extension.
- Go **broad → specific → variant** in the descriptor.
- Increment version **only when pixels/samples change**.

**Don’t**
- Don’t use `final`, `new`, `copy`, dates in the name.
- Don’t mix case or punctuation (`# % & ? ! @`).
- Don’t reorder concepts (`Cactus_Enemy` instead of `Enemy_Cactus`).

---

## Correct vs Incorrect
| ✅ Correct | Why | ❌ Incorrect | Why |
|---|---|---|---|
| `ART_Enemy_Cactus_Front_v1.png` | Follows pattern; clear order | `enemy cactus front FINAL.png` | Spaces + no versioning convention |
| `AUD_Loop_Forest_v2.ogg` | Type + purpose + version | `forestloop2.OGG` | Missing TYPE; wrong case |
| `UI_Button_Start_v1.png` | Human-readable, sortable | `uiBtnStart.png` | Jargon + camelCase |

---

## Versioning rules
- **Start:** `v1` for the first shareable file.
- **Bump:** content edits (visual/audio changes) → `v2`, `v3`, …
- **Don’t bump:** metadata-only changes (license, notes, tags).
- **Variants:** optional short tag before version: `_AltA`, `_AltB`
  - Example: `ART_Enemy_Cactus_Front_AltA_v1.png`

---

## Extensions (lowercase)
- Images: `png`, `jpg`, `svg`, `psd`
- Audio: `wav`, `ogg`, `mp3` *(prefer `wav` masters; `ogg` for runtime)*
- Data/Docs: `json`, `csv`, `md`, `pdf`

---

## Accessibility (WCAG-aligned)
- Underscores are screen-reader friendly; avoid camelCase abbreviations.
- Use **plain words** a non-specialist understands.
- Keep names short to prevent truncation in UIs and tooltips.

---

## Validation (pre-commit checklist)
- Name matches: `TYPE_Descriptor_v#.<ext>`
- TYPE is **ART / AUD / UI**
- Descriptor uses **Title_Case** + **underscores**
- Version present and correct (`v1`, `v2`, …)
- Extension lowercase
- Length ≤ 30 chars (before `.ext`)

*(Optional regex you can use in linters/validators)*  
^(ART|AUD|UI)[A-Z][A-Za-z0-9]*(?:[A-Z][A-Za-z0-9])_v[1-9][0-9]*.[a-z0-9]+$


---

## Governance
- If you rename a file, update `final_filename` in your metadata table.
- Run a weekly audit (script or filter) to flag non-conforming names.
- Record exceptions and rationale in `/logs/validation-notes.md`.

---

## Change Log
| Version | Date | Summary | Author |
|---|---|---|---|
| v1 | 2025-11-02 | Initial convention for ART/AUD/UI assets. | KU |
