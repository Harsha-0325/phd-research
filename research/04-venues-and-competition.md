# 4. Venues, Acceptance Rates and How Competitive This Field Is

*Compiled September 2026 from official conference announcements and reports. Links below.*

## Acceptance rates of the conferences in our plan

| Venue | Year | Submissions | Accepted | Acceptance rate | Tier (rough) |
|-------|------|-------------|----------|-----------------|--------------|
| ICML (for reference only) | 2025 | 12,107 | 3,260 | **26.9%** | Top (A*) |
| NeurIPS Datasets & Benchmarks | 2024 | — | — | **25.3%** (2025 aligned with main track) | Top (A*) |
| IEEE ICIP | 2025 | ~2,000 | 498 | **~25%** | Solid (B / A−) |
| BMVC | 2025 | 865 | 276 | **31.9%** | Good (A−/B) |
| WACV | 2025 | 2,458 | — | **37.8%** | Good (A−/B) |
| IJCNN | 2025 | 5,526 | 2,152 | **38.9%** | Mid (B) |
| ICMLA | — | — | — | not published | Mid (C/B) |
| CVPR VAND workshop | 2026 | — | — | not published | Workshop, **archival** (in CVPR proceedings) |
| AI4Mat workshop (NeurIPS/ICLR) | 2025 | — | 115 accepted | not published | Workshop, **NON-archival** ⚠️ |

**In plain words:** at a good international conference, **60–75% of papers get rejected.** A first-time
submission is more likely to be rejected than accepted. That's normal. Most good papers get rejected once,
improve from the reviews, and get in at the next venue. Plan for **two submission rounds per paper.**

⚠️ **AI4Mat is non-archival.** Accepted papers aren't formally published, so it probably
**won't count** toward a PhD's publication requirement. Use it for feedback and visibility, and submit the full paper
to an archival venue.

## The AI boom effect (why it's harder now than 3 years ago)

- **IJCNN submissions doubled in a single year** (about +100% in 2025). WACV and ICIP keep setting new records.
- AI tools make it cheap to produce "we applied model X to dataset Y" papers, so reviewers now see many of them and reject them quickly.
- **What still gets accepted:** a *new question*, a *new dataset or benchmark*, a *method that is justified* (not just swapped in), and honest evaluation.
  Our plan in file 03 is built around exactly those.

## How big is *this* domain (DL + X-ray CT of metals)?

- **Growing fast, but mostly in journals, not CS conferences.** Most papers appear in materials and manufacturing journals
  (*Materials Characterization*, *Additive Manufacturing*, *npj Computational Materials*, *Engineering Fracture Mechanics*, *J. Nondestructive Evaluation*).
  A 2024 review in *CIRP J. Manufacturing Science & Technology* covers ML in industrial CT as its own sub-field.
- **Few papers in CS conferences.** In-domain conference examples we found were mostly IEEE ICIP (e.g. the ORNL accelerated industrial CT work, ICIP 2023).
  - **Good news:** little *direct* competition from the CV/ML crowd.
  - **Bad news:** CS-conference reviewers may not know materials science, so the paper must explain the problem simply and show why it matters.

### Most recent papers we found (2026)

*Month and venue are as listed on the publisher/arXiv page. Please verify before citing.*

**Journal papers**
- Direct 3D segmentation and classification of defects in metal AM using multi-scale DL on XCT (*Materials Characterization*, 2026): https://www.sciencedirect.com/science/article/abs/pii/S1044580326005978
- GNN assessment of fatigue-critical pores (*npj Computational Materials*, 2026): https://www.nature.com/articles/s41524-026-02148-0
- Curvature-based defect features for fatigue life prediction in LPBF (*Progress in Additive Manufacturing*, 2026): https://link.springer.com/article/10.1007/s40964-026-01771-z
- In-situ X-ray CT of micro-voids in S355/S690/S960 steel (*Construction and Building Materials*, 2026): https://www.sciencedirect.com/science/article/abs/pii/S0950061826002217
- Ductile fracture of Q550 steel with μCT + digital volume correlation (*Engineering Fracture Mechanics*, 2026): https://www.sciencedirect.com/science/article/abs/pii/S0013794426000469

**Preprints / conference-track**
- XCT-SAM: domain adaptation of SAM for industrial XCT defects (arXiv, July 2026): https://arxiv.org/html/2607.14287v1
- Interpretable CV for defects in X-ray tomography of SiC/SiC composites (arXiv, May 2026): https://arxiv.org/abs/2605.20159
- VAND 4.0 industrial anomaly challenge at CVPR 2026 (2D images, not CT): https://arxiv.org/abs/2605.14808

## Is this college-level or PhD-level?

| Level | Example in this domain |
|-------|------------------------|
| Course / BTech project | Train a U-Net to segment pores in a public CT dataset; report Dice |
| Master's thesis | Compare 3–4 segmentation models, add augmentation, analyse errors |
| **PhD paper** | Ask a *new question* (e.g. predict mechanical state with guaranteed uncertainty), build a *new benchmark*, or give a *method with physical justification*, and evaluate it honestly (grouped CV, strong baselines) |

"Apply a CNN to the steel dataset and report accuracy" sits between the first two rows. That's why the plan in file 03 changes the *question*, not just the model.

## Sources
- ICIP 2025: https://2025.ieeeicip.org/
- BMVC 2025: https://bmvc2025.bmva.org/programme/accepted_papers/
- WACV 2025 stats: https://x.com/wacv_official/status/1895861501963223288
- IJCNN 2025 review-process report: https://arxiv.org/abs/2603.19244
- NeurIPS D&B chairs' blog: https://blog.neurips.cc/2025/09/30/reflecting-on-the-2025-review-process-from-the-datasets-and-benchmarks-chairs/
- ICML 2025: https://csconfstats.xoveexu.com/conferences/icml/2025/
- AI4Mat-NeurIPS-2025: https://sites.google.com/view/ai4mat/ai4mat-neurips-2025
- VAND 4.0 @ CVPR 2026: https://sites.google.com/view/vand4-cvpr2026
- ML in industrial X-ray CT review: https://www.sciencedirect.com/science/article/abs/pii/S1755581724000634
