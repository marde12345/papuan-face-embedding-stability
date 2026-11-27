# papuan-face-embedding-stability

Aggregate result tables for the manuscript:

> A. A. Arman, M. F. Aza, F. Hidayat, F. A. Alunjati, L. Mahardini, F. F. Lubis, and S. H. Supangkat, "Analysis of Face Embedding Stability under Melanin-Aware and Luminance Preprocessing across Facial Image Brightness in Uncontrolled Video," manuscript prepared for *IEEE Access*.

**Status:**
- This is a local staging copy prepared on 27-11-2026, pending author review.
- It has not been pushed or published, and no repository or DOI exists yet.
- The manuscript has not been published.

## Project description
- **The study:** it examines how two image-preprocessing methods change the embeddings of a frozen, pretrained face recognition model (InsightFace `w600k_r50`) on face crops from one uncontrolled video. The methods are:
  - a reconstruction of the routed Melanin-Aware preprocessing;
  - a unified luminance enhancement.
- **What is measured:** because the footage has no identity labels, the study measures **embedding stability**, not verification accuracy. It uses 359 same-tracklet crop pairs that two reviewers judged to show the same person, against 494 different-face pairs from the same frame.

## Contents
```
README.md              this file
DATA_DICTIONARY.md     method codes, column definitions, mapping to manuscript tables
DATASET_REVIEW.md      what data exists, what is included or excluded, and pending approvals
MANIFEST.sha256        SHA-256 checksums of every included file (check with: shasum -a 256 -c MANIFEST.sha256)
.gitignore
data/embedding_stability/      10 CSV tables: Tables 2–6 and sensitivity analyses
data/preprocessing_latency/    1 CSV table: Table 8
face_crops/                    1,599 PNG face crops (identifiable, not anonymized) + README.md + SHA256.txt
```
**`face_crops/`** holds the 1,599 face crops used in the analysis, added with the supervisor's permission as reported by the researcher. The faces are identifiable and were not anonymized. See `face_crops/README.md`. All files in `data/` are **aggregate tables**. The repository contains no video, embeddings, per-pair scores, identifiers or timestamps. Method codes are `B1` (unenhanced baseline), `A` (Melanin-Aware reconstruction) and `B3` (luminance enhancement). See `DATA_DICTIONARY.md`.

## What this repository supports
- **Supports:** checking the values reported in Tables 2–6 and 8 of the manuscript, and seeing statistics that the text reports only in part.
- **Does not support:**
  - **recomputing the results:** the video, pair lists and landmarks are not included;
  - **Table 7** (held-out operating point): its source is marked internal-only, see `DATASET_REVIEW.md`;
  - **Figs. 3–4:** these are drawn from per-pair similarities.

No code is included. The analysis scripts depend on restricted data and hard-code private paths.

## Limitations
- **One source:** one uncontrolled video, one pretrained model, and a preprocessing reconstruction with assumed parameters.
- **Stability only:** the results concern embedding stability. They do not establish recognition performance, verification accuracy or fairness for any population.
- **Weak pairs:** same-tracklet pairs rest on human visual judgement. They are not verified identities. Different-face pairs are easy controls.
- **Brightness is not skin tone:** brightness quartiles describe image brightness only.
- **Latency:** values are specific to one machine (Apple M1 Pro) and an unoptimised implementation.

## Citation
Please cite the manuscript above.
- **Publication details:** journal volume, pages and article DOI are **pending** until publication.
- **Dataset DOI:** **pending**. No DOI has been issued for this data. Add one only after an archive (for example Zenodo) has actually issued it.

## Licence
**Pending.** No licence has been chosen. Without one, default copyright applies. The authors should choose a licence before publishing, for example CC BY 4.0 for the data tables.
