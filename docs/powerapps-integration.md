# Power Apps Integration & Roadblocks (Asset Atlas)

_Last updated: November 2025_

## Purpose
This document records the intended Power Apps to Power Automate to Typesense integration for **Asset Atlas**, and the admin restrictions that prevented live deployment.  
The prototype uses an **Excel data source** to simulate live search results while keeping the UX, accessibility, and filter logic identical to the target design.

---

## Intended End-State Architecture

Power Apps (Canvas App)  
- **Power Automate Flow** (HTTP - Typesense `/documents/search`)  
- **Typesense Cluster** (hosted index for asset metadata)  
- JSON response bound to the gallery (`colResults`).

Supporting services explored:  
- **SharePoint List** – as a governed vocabulary source.  
- **OneDrive Excel** – initial mock dataset for development.

---

## Exploration Summary

| System | Goal | Outcome | Notes |
|:--|:--|:--|:--|
| **Typesense** | Host search index for asset metadata. | Success: Working via Postman and curl tests. | Cluster responds to health & search endpoints. See [`typesense-config.md`](./typesense-config.md). |
| **Power Automate (HTTP)** | Securely query Typesense and return JSON to Power Apps. | Roadblock: Blocked by tenant DLP policy. | HTTP connector disabled; custom connector not permitted without admin approval. |
| **SharePoint Lists** | Replace Excel with governed data and delegation. | Read-only access only. | List creation restricted; no write privileges for app maker role. |
| **Power Apps (Excel)** | Build functional UX using mock dataset. | Success: Implemented and stable. | Substring search, category filter (`art / ui / audio`), clear/reset logic, and accessibility testing completed. |

---

## Current Mock Implementation

- **Data Source:** Excel table `AssetsTable` (local).  
- **Logic:** Filter on `display_name` (substring, 1-char guard) + `category`.  
- **UI:** Search box, category dropdown, clear button, results gallery.  
- **Accessibility:** Tab order 0-3, visible focus, contrast ≥ 4.5:1, empty-state labels.  
- **Compliance:** No secrets stored client-side; DLP-safe prototype.

---

## Desired Future Implementation

1. **Re-enable or approve HTTP connector** within tenant policy.  
2. Create **Power Automate Flow** that:
   - Accepts `q`, `category`, `license`, `owner` as inputs.  
   - Performs GET to `/collections/asset_atlas/documents/search`.  
   - Returns parsed JSON to Power Apps (`colResults`).  
3. Replace local `colAllAssets` with Flow output.  
4. Extend filters to include `license` and `owner`.  
5. Optionally move reference data (categories, licenses) to SharePoint Lists or Dataverse.

---

## Lessons & Constraints

- **Tenant DLP Policies:** HTTP and custom connectors require explicit admin approval within current development environment. 
- **Excel Connector:** Non-delegable for text search; row limit ≈ 2 000.  
- **Power Apps Search:** Prefix search (StartsWith) replaced with substring (Find) for better usability.  
- **Data Normalization:** `Trim()` and `Lower()` applied to prevent whitespace or case mismatch.  
- **Outcome:** UX and accessibility fully validated; backend integration deferred pending admin clearance.

---

## Next Steps

- [ ] Migrate `AssetsTable` to a governed source (SharePoint or Dataverse).  
- [ ] Create approved connector or Flow for Typesense.  
- [ ] Update gallery bindings to live `colResults`.  
- [ ] Retest accessibility and performance.  
- [ ] Update `SETUP.md` and `typesense-config.md` once live integration is confirmed.

---

## References
- [`typesense-config.md`](./typesense-config.md) — Cluster endpoints & schema.  
- [`SETUP.md`](./SETUP.md) — Environment setup instructions.  
- [`field-values-v1.md`](./field-values-v1.md) — Dropdown vocabularies.  
- [`tech-summary.md`](./tech-summary.md) — Technology rationale and toolchain.  

---

> **Summary:**  
> Live integration was fully planned, tested in isolation, and deferred only due to administrative policy limits.  
> The mock Excel build stands as a complete UX and accessibility prototype, ready to connect to Typesense once approvals are granted.
