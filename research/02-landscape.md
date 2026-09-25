# 2. Landscape: Where Deep Learning Meets Imaging of Metals

We deliberately looked **beyond** the one dataset. That meant other imaging physics (X-ray CT, 2D radiography,
neutron imaging), other "metal-like" materials (lithium metal in batteries, corrosion), and other
ML problem types (segmentation, prediction, anomaly detection, reconstruction, uncertainty).

**Crowdedness scale:** 🔴 crowded (hard to stand out) · 🟠 active (possible, needs a sharp angle) · 🟢 thin (real opening)

## Summary table

| # | Sub-area | Crowdedness | Fit for a CS/DL person | Public data? |
|---|----------|-------------|------------------------|--------------|
| A | 2D X-ray radiography: weld / casting defect detection | 🔴 | High | Yes (many) |
| B | Pore segmentation in 3D CT of 3D-printed (additive manufacturing, AM) metal | 🔴 | High | Yes (NIST) |
| C | Foundation models (SAM) for industrial CT defects | 🟠 | Very high | Yes |
| D | Fatigue life prediction from CT pore statistics (AM parts) | 🟠 | Medium | Partial |
| E | Fast / sparse-view CT reconstruction for metal parts | 🟠 | High, but needs recon-physics depth | Rarely (needs raw projections) |
| F | Lithium-metal battery dendrites in X-ray CT | 🟠 | High | Limited |
| G | Corrosion pits in 3D CT | 🟠→🟢 | High | Limited |
| H | Void tracking / damage evolution in 4D (in-situ) CT | 🟢 | Medium | Rare |
| **I** | **Predicting mechanical state (strain, fracture progress) from a CT scan** | 🟢 | **Very high** | **Yes (our dataset)** |
| **J** | **Calibrated uncertainty for CT-based damage prediction** | 🟢 | **Very high** | **Yes** |
| **K** | **Unsupervised anomaly detection on 3D industrial CT *volumes*** | 🟢 | **Very high** | **Buildable from public sets** |
| L | Neutron imaging / neutron + X-ray fusion with DL | 🟢 | High | Hard to get |

## Notes per area (with key sources)

### A. 2D radiography of welds/castings 🔴
Hundreds of CNN/YOLO papers. It's easy to publish in low-tier venues and hard to make an impact. **Avoid.**

### B. AM pore segmentation in CT 🔴
U-Net and 3D U-Net on NIST additive-manufacturing CT data is well trodden.
- NIST U-Net AM segmentation: https://tsapps.nist.gov/publication/get_pdf.cfm?pub_id=930890
- Multi-scale 3D segmentation on XCT (2026): https://www.sciencedirect.com/science/article/abs/pii/S1044580326005978

### C. Segment Anything (SAM) for industrial CT 🟠
Very active in 2024–2026. Several groups have already adapted SAM to AM CT. Only enter with a very specific angle.
- Unsupervised promptable porosity segmentation with SAM (npj Adv. Manuf. 2025): https://www.nature.com/articles/s44334-025-00021-4
- SAM fine-tuned on GAN-simulated data (2024): https://arxiv.org/abs/2412.11381
- XCT-SAM, parameter-efficient domain adaptation (2026): https://arxiv.org/html/2607.14287v1

### D. Fatigue life from CT defects 🟠
Active, mostly in AM alloys (Ti, IN718). Mostly tabular ML on "largest pore size" features. There is a GNN paper from 2026.
- GNNs for fatigue-critical pores (npj Comput. Mater. 2026): https://www.nature.com/articles/s41524-026-02148-0
- Defect-driven physics-informed NN (Phil. Trans. A): https://royalsocietypublishing.org/rsta/article/381/2260/20220386/41296/Defect-driven-physics-informed-neural-network

### E. Sparse-view / accelerated industrial CT 🟠
Strong groups (e.g. Oak Ridge National Lab) own this. It needs raw projection data and reconstruction-physics expertise.
- DL workflow for accelerated industrial XCT: https://arxiv.org/html/2309.14371
- Plug-and-play 2.5D artifact-reduction prior (2025): https://arxiv.org/pdf/2506.14719

### F. Lithium-metal dendrites (X-ray CT) 🟠
A "metal" that CS people often overlook. There are a few segmentation papers, and data access is limited.
- Transformer–CNN dendrite segmentation: https://arxiv.org/abs/2302.04824
- Operando Li plating with ML (npj Comput. Mater. 2023): https://www.nature.com/articles/s41524-023-01039-y

### G. Corrosion in 3D CT 🟠→🟢
Emerging, with a handful of 2025 papers. Materials groups do the work, and DL is used as a tool rather than as the contribution.
- Localized corrosion segmentation (npj Mater. Degrad. 2025): https://www.nature.com/articles/s41529-025-00633-3
- Pitting in Al wires pipeline (Adv. Eng. Mater. 2025): https://advanced.onlinelibrary.wiley.com/doi/10.1002/adem.202401699

### H. 4D void evolution 🟢 (but data is scarce)
Mostly materials-science papers using classic image processing or basic U-Nets. There's almost no *learning* of the dynamics.
- 4D void tracking algorithm: https://www.sciencedirect.com/science/article/abs/pii/S2352492822007486
- Al6061 in-situ CT + NN segmentation (FFEMS 2023): https://onlinelibrary.wiley.com/doi/10.1111/ffe.13904
- 4D-ONIX, 3D movies from sparse projections (2025): https://www.nature.com/articles/s44172-025-00390-w

### I. Mechanical state from a CT scan 🟢 ← *directly on our dataset*
Essentially **one line of work** on this exact problem: Tiong *et al.* 2023 (persistent homology + DL).
Nobody (in our searches) has compared learned 3D representations, set/graph models of the void
population, or tested transfer between loading types.
- Tiong 2023: https://arxiv.org/abs/2205.09075
- Related (stress fields from CT, CMAME 2024): https://www.sciencedirect.com/science/article/pii/S0045782524001348

### J. Calibrated uncertainty 🟢
Uncertainty for CT segmentation exists (e.g. thermal-spray coatings), and conformal prediction exists for
remaining-life estimation from **sensor time series**. We did **not find** conformal / calibrated
uncertainty applied to *damage-state prediction from CT volumes*. For safety-critical steel, that matters:
an engineer needs "strain = 0.3 ± 0.05 with 90% guarantee", not just "0.3".
- Segmentation with uncertainty (thermal spray CT): https://www.osti.gov/pages/biblio/1975896
- Conformal prediction for remaining useful life: https://arxiv.org/abs/2212.14612

### K. Unsupervised anomaly detection on CT volumes 🟢
Industrial anomaly detection (the MVTec family) is huge in computer vision, but its 3D benchmarks are **point clouds / surface scans**,
not internal CT volumes. Medical CT has anomaly benchmarks (BMAD). We did **not find** a public
benchmark for *volumetric industrial CT* anomaly detection. That is a classic CS-venue contribution:
a benchmark plus a baseline method.
- MVTec 3D-AD (point clouds): https://arxiv.org/abs/2112.09045
- BMAD medical AD benchmark: https://arxiv.org/abs/2306.11876
- Supervised CT casting defect detection (not unsupervised): https://www.researchgate.net/publication/365262233
- Public CT sources to build from: NIST CoCr AM XCT (https://www.nist.gov/el/intelligent-systems-division-73500/cocr-am-xct-data),
  NIST simulated XCT with ground-truth pores (https://catalog.data.gov/dataset/simulated-x-ray-computed-tomography-xct-and-ground-truth-images-of-cylindrical-sample-with),
  NIST GAN-generated lack-of-fusion pores (https://data.nist.gov/pdr/lps/ark:/88434/mds2-3963),
  and our steel dataset.

### L. Neutron imaging (the "other rays") 🟢 but hard
Neutrons see hydrogen inside metals (hydrogen embrittlement). There's very little DL work, but
public data is scarce and beamtime is hard to get. Keep this as a **future-work / 3rd-paper** idea.
- Neutron imaging of hydrogen in metals, review (2025): https://www.oaepublish.com/articles/microstructures.2025.74
- NIST NeXT neutron + X-ray system: https://www.nist.gov/programs-projects/imaging-neutron-and-x-ray-tomography-next-system
- Diffusion-model neutron/X-ray fusion (2026): https://www.sciencedirect.com/science/article/pii/S168785072600381X
