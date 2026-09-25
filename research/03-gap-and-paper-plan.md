# 3. The Gap and the Two-Paper Plan

## The one-paragraph version

Most "deep learning + X-ray + metal" papers answer **"where is the defect?"** (segmentation/detection).
That space is crowded. Two questions are much less explored and fit a CS/DL skill set perfectly:

1. **"How damaged is this steel, and how sure are we?"** Predict the mechanical state (strain, fatigue
   progress) from a CT scan, with a **guaranteed confidence interval**. → *Paper 1, uses the steel dataset she already has.*
2. **"Can we flag abnormal defects without anyone labelling them?"** Unsupervised anomaly detection
   on **3D CT volumes**, which has no public benchmark yet (in our searches). → *Paper 2, a benchmark plus a method, suited to a CS venue.*

Suggested thesis umbrella:
> **Label-efficient and trustworthy deep learning for X-ray computed tomography of metals**

Both papers live under this umbrella, and paper 1 grows naturally out of the work she has already shown her professor.

---

## Paper 1: Damage-state prediction from CT with learned void representations and calibrated uncertainty

### The gap
- On this exact problem there is essentially **one prior method**: Tiong *et al.* 2023 (persistent homology + DL, MAE 0.09 / 0.14).
- It uses **hand-crafted topology features**. Nobody has tested whether **learned** representations
  of the void population do better, or looked at *which* voids drive the prediction.
- It gives **point predictions only**. For structural steel, a prediction with no reliable error bar is
  hard to trust. We found no work applying **conformal prediction** to CT-based damage estimation.
- The dataset is **new (2025)**. Apart from the group that created it, nobody has published on it yet (as far as our searches show).

### Research questions
- **RQ1 (representation):** Given the same CT data, do learned models (set / graph / 3D CNN) match or beat hand-crafted topology features?
- **RQ2 (trust):** Can we produce prediction intervals with a *guaranteed* coverage (e.g. true strain inside the interval 90% of the time)?
- **RQ3 (transfer and insight):** Does a model trained on tensile damage say anything about fatigue damage? Which voids matter most?

### Why a graph model is a *physics-motivated* choice (reviewers like this)
Steel breaks in three stages: tiny voids **nucleate**, then **grow**, then **coalesce** (link up) into a crack.
Coalescence depends on **how close voids are to each other**. A graph whose nodes are voids and whose edges connect
nearby voids encodes exactly that. So the model is designed around the known physics rather than chosen at random,
and that turns a "method swap" into a *justified* contribution.

### Experiments (all fit on a single GPU)
| Group | Model | Input |
|-------|-------|-------|
| Baselines | XGBoost / MLP | the provided tabular metrics |
| Baseline (reproduced) | PH + DL (Tiong 2023, ported to PyTorch) | persistence diagrams |
| **Set model** | DeepSets / PointNet / Set Transformer | each void = a point (position, volume, shape descriptors) |
| **Graph model** | GNN (GCN / GAT / GIN) on a k-nearest-neighbour void graph | same, plus void-to-void distances |
| 3D CNN (if raw volumes are available) | small 3D ResNet with rotation augmentation | CT volume / patches |
| **Uncertainty** | deep ensembles, MC dropout, **split conformal**, **conformalized quantile regression** | on top of the best models |

**Evaluation:**
- MAE / R² for strain and fracture progress; accuracy / F1 for HCF / LCF / ULCF.
- For uncertainty: coverage, interval width, calibration error.
- **Grouped cross-validation by specimen.** Patches from the same bar must never appear in both train and test.
  This is a very common hidden leak in materials-ML papers, and pointing it out is a contribution by itself.
- Explainability: node-importance / attention maps showing *which voids* drive the prediction.

### Honest risks
- **Small data** (276 samples). Mitigation: set and graph models are parameter-light; use repeated grouped CV and report variance.
- **The files may not include raw volumes.** If Dryad only has extracted defect data, drop the 3D CNN row. The set and graph models still work.
- **Learned models might not beat PH.** That's still publishable *if* we pair it with the uncertainty and transfer results
  ("PH is a strong prior; here is when learned models help, and here is how to trust either one").

### Where to submit
International conferences, which is what her professor asked for: IEEE ICIP (~25% acceptance), IJCNN (~39%) or ICMLA.
The **AI4Mat** workshop is good for early feedback but is **non-archival**, so it likely won't count as a publication.
A journal extension would suit *Computational Materials Science* or *Integrating Materials and Manufacturing Innovation*.
See [file 04](04-venues-and-competition.md) for acceptance rates. *(Check the current deadlines before committing to one.)*

---

## Paper 2: A benchmark for unsupervised anomaly detection in industrial CT volumes

### The gap
- Industrial anomaly detection (the MVTec family, PatchCore, EfficientAD, …) is one of the busiest topics in computer vision.
- But its "3D" benchmarks are **surface point clouds**. They never look *inside* the part.
- Medical imaging has CT anomaly benchmarks (BMAD). **Industrial / materials CT does not**, based on our searches.
- In practice, nobody wants to hand-label every pore in every CT scan. "Learn what normal material looks like
  and flag anything unusual" is exactly what industry needs.

### What we would build
1. **Benchmark:** curate public CT volumes (NIST CoCr AM, NIST simulated ground-truth pores, NIST GAN
   lack-of-fusion pores, the steel dataset). Define "normal" as material with acceptable background porosity, and
   "anomalous" as critical defects: large lack-of-fusion pores, cracks and clustered voids. Use real labelled defects where available,
   and physics-realistic **synthetic insertion** otherwise.
2. **Baselines:** 2D anomaly-detection methods applied slice-by-slice (PatchCore, PaDiM, EfficientAD), 2.5D versions,
   a 3D autoencoder, and a diffusion-based reconstruction model.
3. **Method:** a simple 3D-aware extension that beats slice-wise baselines, e.g. 3D patch memory banks or
   foundation-model features lifted to 3D.
4. **Metrics:** voxel-level AUROC, 3D region overlap (AUPRO), object-level defect recall.

### Honest risks
- **Every metal sample has *some* pores,** so "normal" has to be defined carefully (by size or shape threshold, or by a
  materials standard). This definition is itself part of the contribution.
- **Synthetic anomalies can be too easy.** Include real defects in the test set.
- **Dataset licences:** check that each source allows redistribution. If one doesn't, ship download-and-prepare scripts instead of the data.

### Where to submit
WACV, BMVC, the CVPR **VAND** (Visual Anomaly and Novelty Detection) workshop, or the **NeurIPS Datasets & Benchmarks** track.

---

## Ideas considered and parked (and why)

| Idea | Why parked |
|------|-----------|
| SAM / foundation models for CT pore segmentation | Several 2024–2026 papers already do this; hard to stand out |
| Weld/casting 2D radiography detection | Very crowded |
| Sparse-view CT reconstruction | Needs raw projection data and reconstruction-physics depth; strong labs already own it |
| Lithium-metal dendrites | Good topic, but little public data |
| Corrosion pits in 3D CT | **Good backup for Paper 2** if a segmentation paper is preferred |
| Neutron / neutron + X-ray imaging | Very thin (good), but data is hard to get. Keep as a 3rd paper or future work |

## Rough timeline

| Weeks | Work |
|-------|------|
| 1–2 | Download data; confirm contents; reproduce Tiong 2023 baseline in PyTorch |
| 3–6 | Set / graph models, grouped CV, conformal intervals |
| 7–8 | Transfer + explainability experiments, figures |
| 9–10 | Write Paper 1 |
| 11+ | Paper 2: benchmark curation → baselines → method |
