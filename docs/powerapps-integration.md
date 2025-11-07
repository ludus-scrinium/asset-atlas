# power apps integration & roadblocks (asset atlas)

_last updated: november 2025_

## purpose
this document records the intended power apps → power automate → typesense integration for **asset atlas**, and the admin restrictions that prevented live deployment.  
the prototype uses an **excel data source** to simulate live search results while keeping the ux, accessibility, and filter logic identical to the target design.

---

## intended end-state architecture

power apps (canvas app)  
- **power automate flow** (http - typesense `/documents/search`)  
- **typesense cluster** (hosted index for asset metadata)  
- json response bound to the gallery (`colresults`)

supporting services explored:  
- **sharepoint list** – as a governed vocabulary source  
- **onedrive excel** – initial mock dataset for development

---

## exploration summary

| system | goal | outcome | notes |
|:--|:--|:--|:--|
| **typesense** | host search index for asset metadata | success: working via postman and curl tests | cluster responds to health & search endpoints. see [`typesense-config.md`](./typesense-config.md) |
| **power automate (http)** | securely query typesense and return json to power apps | roadblock: blocked by tenant dlp policy | http connector disabled; custom connector not permitted without admin approval |
| **sharepoint lists** | replace excel with governed data and delegation | read-only access only | list creation restricted; no write privileges for app maker role |
| **power apps (excel)** | build functional ux using mock dataset | success: implemented and stable | substring search, category filter (`art / ui / audio`), clear/reset logic, and accessibility testing completed |

---

## current mock implementation

- **data source:** excel table `assetstable` (local)  
- **logic:** filter on `display_name` (substring, 1-char guard) + `category`  
- **ui:** search box, category dropdown, clear button, results gallery  
- **accessibility:** tab order 0–3, visible focus, contrast ≥ 4.5:1, empty-state labels  
- **compliance:** no secrets stored client-side; dlp-safe prototype

---

## desired future implementation

1. **re-enable or approve http connector** within tenant policy  
2. create **power automate flow** that:  
   - accepts `q`, `category`, `license`, `owner` as inputs  
   - performs get to `/collections/asset_atlas/documents/search`  
   - returns parsed json to power apps (`colresults`)  
3. replace local `colallassets` with flow output  
4. extend filters to include `license` and `owner`  
5. optionally move reference data (categories, licenses) to sharepoint lists or dataverse

---

## lessons & constraints

- **tenant dlp policies:** http and custom connectors require explicit admin approval within current development environment  
- **excel connector:** non-delegable for text search; row limit ≈ 2 000  
- **power apps search:** prefix search (startswith) replaced with substring (find) for better usability  
- **data normalization:** `trim()` and `lower()` applied to prevent whitespace or case mismatch  
- **outcome:** ux and accessibility fully validated; backend integration deferred pending admin clearance

---

## next steps

- [ ] migrate `assetstable` to a governed source (sharepoint or dataverse)  
- [ ] create approved connector or flow for typesense  
- [ ] update gallery bindings to live `colresults`  
- [ ] retest accessibility and performance  
- [ ] update `setup.md` and `typesense-config.md` once live integration is confirmed

---

## references
- [`typesense-config.md`](./typesense-config.md) — cluster endpoints & schema  
- [`setup.md`](./setup.md) — environment setup instructions  
- [`field-values-v1.md`](./field-values-v1.md) — dropdown vocabularies  
- [`tech-summary.md`](./tech-summary.md) — technology rationale and toolchain  

---

> **summary:**  
> live integration was fully planned, tested in isolation, and deferred only due to administrative policy limits.  
> the mock excel build stands as a complete ux and accessibility prototype, ready to connect to typesense once approvals are granted.

