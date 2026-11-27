# Dataset review (27-11-2026)

- **What this is:** a staging copy for a Git repository. Nothing has been pushed or published.
- **Repository visibility:** not yet decided. Anything committed to Git can be cloned and stays in the history even after deletion, so the inclusion bar here is higher than for a restricted Drive folder.

## Included
- **Data:**
  - 11 aggregate CSV tables (`data/`);
  - 10 embedding-stability tables from the 359-pair identity-validated analysis;
  - 1 preprocessing-latency summary.
- **Copies:** byte-identical to the project outputs. Checksums are in `MANIFEST.sha256`.
- **Why they are shareable:**
  - **Aggregate only:** every row is a method, subset, statistic or resampling scheme.
  - **No identifiers:** a scan found no pair, crop or track IDs, timestamps, paths, source names or "private" markers.
  - **Match the manuscript:** values were spot-checked against Tables 2, 3, 5 and 6, including the AUC and d′ confidence intervals of Table 2.
- **Documentation:** `README.md`, `DATA_DICTIONARY.md`, this file, `MANIFEST.sha256` and `.gitignore`.

## Face crops: excluded
**What exists:**
- 24,216 detector crops in the project;
- of these, 1,599 crops used in the analysis;
- review sheets, context frames and contact sheets.

The crops show identifiable faces, and there is no consent record for the footage.

**Current approval:**
- The researcher reported that the supervisor approved adding the 1,599 analysed crops to a **Google Drive** data package, shared with named recipients.
- That package (renamed files, no mapping) exists separately.
- No written approval document is in the repository.

**Why they are not in this Git package:**
1. **Scope:** the reported approval covers a restricted Drive folder. It does not clearly cover a Git repository, whose visibility is undecided and whose history is permanent.
2. **The manuscript:** it states that face crops are not publicly released, and that any face image added later would be anonymized sufficiently to prevent identification.
3. **Repository size:** the crops would add about 93 MB of binary images. Large binaries suit an archive or Git LFS better than plain Git.

**Approval needed before any crop enters a repository:** written confirmation from the supervisor, and from the institution if required, covering:
- (a) Git or archive hosting of these specific 1,599 identifiable images;
- (b) the repository visibility (private with named collaborators, or public);
- (c) the consent or permission basis, given that no consent record exists;
- (d) if public: what anonymization is required, as the manuscript commits to. Note that anonymized crops no longer reproduce the embedding results.
- **Also needed if public:** a revised data-availability statement in the manuscript.

### Update 27-11-2026: GitHub repository created by the researcher (nothing pushed)
- **Request:** the researcher asked to add the face crops to this staging package if documented permission supports it.
- **What was checked:**
  - the project documentation in `docs/` and the research report folders;
  - the supplied documents in `data/raw/documents/`;
  - the Drive package review.
- **Result:** **no document authorizes sharing these face images in a Git repository.**
  - The only approval is the supervisor approval reported by the researcher for a restricted Drive folder. It is not documented in writing in the project, and it does not mention Git, GitHub or public visibility.
  - The manuscript states that face crops are not publicly released.
- **Decision:** no images copied. `face_crops/` contains only a README explaining this.
- **Exact approval still needed:** written confirmation from the supervisor (and the institution, if required), stating:
  1. that the face crops may be hosted in the GitHub repository;
  2. **which images**: for example the 1,599 analysed crops from the project's internal crop folder, or another defined set;
  3. the repository **visibility** (private with named collaborators, or public) and who may be given access;
  4. the **consent or permission basis**, since no consent record exists;
  5. whether **anonymization** is required. The manuscript commits to it for any face image added later. Cropping is not anonymization;
  6. whether the **original filenames** may be kept. They encode the video frame number, from which each face's time in the video can be derived, which conflicts with the no-timestamp rule;
  7. if public, that the manuscript's data statement will be revised.

### Update 27-11-2026 (later): crops added
- **Permission:** the researcher reported that the supervisor has given permission to add the face crops to this repository. The permission is recorded as reported; no written document is in the project.
- **What was added:** `face_crops/` with the same 1,599 analysed crops as the Drive package (random-order neutral names, byte-identical copies, `face_crops/SHA256.txt`, about 92 MB).
- **Still applies:**
  - the faces are identifiable and not anonymized;
  - no consent record exists;
  - the manuscript says face crops are not publicly released. A public repository conflicts with that statement unless the manuscript is revised.
- **Still recommended:** keep the written permission on file.

## Other exclusions
| Material | Reason |
|---|---|
| Raw video, face embeddings | Restricted. Embeddings could support re-identification. |
| Per-pair similarities, pair lists, X4 split and pair scores | Pair-level data with pair, crop or group IDs |
| Crop and frame metadata, tracklets, landmarks, timestamps | Identifying or source-revealing |
| Reviewer annotations and review sheets | Pair-level, and sheets contain faces and whole frames |
| Table 7 source (X4 `results.json`, `REPORT.md`) | Marked "internal use only, never publish". Needs approval for an aggregate-only summary. |
| Analysis scripts | Depend on restricted data, hard-code private dataset paths and the video filename, and reveal the crop-ID format. Sharing them needs approval and a review to remove those paths. |
| Exploratory experiments (X5, X6) | Not part of the manuscript |

## Pending decisions
1. **Repository:** visibility (private or public) and the owner account.
2. **Licence** for the data tables.
3. **Face crops:** whether any are allowed in the repository; see the approval needed above.
4. **Table 7:** whether an aggregate-only summary may be added.
5. **Code:** whether redacted analysis scripts should be added.
6. **DOI:** pending until an archive actually issues one. Do not add a placeholder DOI.
