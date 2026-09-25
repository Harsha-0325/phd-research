# 1. The Reference Dataset (what she has been working with)

## The paper

**"Internal defect database of mechanically deformed ferritic steel via X-ray computed tomography"**
Lee, Gunjick; Yi, Gyeong Hoon; Tiong, Leslie Ching Ow; *et al.* — *Scientific Data* (Nature), 2025.

- Article: https://www.nature.com/articles/s41597-025-06141-y
- Open-access copy (PMC): https://pmc.ncbi.nlm.nih.gov/articles/PMC12663453/
- Data (Dryad): https://datadryad.org/dataset/doi:10.5061/dryad.9cnp5hqpf  (DOI `10.5061/dryad.9cnp5hqpf`)

## What is in it (in computer-science terms)

Steel bars were pulled (tensile test) or shaken back and forth many times (fatigue test)
until they were damaged. Each sample was then scanned with X-ray CT. That gives a **3D grayscale
volume**, where tiny dark holes ("voids" / "defects") are the damage.

| Subset | Samples | Defect records | Label you can predict |
|--------|---------|----------------|-----------------------|
| Tensile | 134 | 938 | **local strain**: how much that region was stretched (regression) |
| Fatigue | 142 | 2,305 | **fracture progress**: how close to breaking (regression / classes) |

- Fatigue samples are split into **high-cycle, low-cycle, ultra-low-cycle** fatigue (a natural 3-class label).
- Fatigue load: R-ratio 0.1, max stress 630–680 MPa.
- Tabular features included per sample: local strain, defect density in three size bins, a "D-value" and a "V-value".
- The defects were described using **persistent homology (PH)**, a topology method (see glossary).

> ⚠️ **To confirm after download:** whether the Dryad files contain the **full raw 3D volumes** or
> only the extracted defects/features. This decides which models we can train (3D CNN on volumes vs.
> set/graph models on defect lists). The network in this cloud session blocks Dryad, so this
> hasn't been checked yet.

## What has already been done with this data

The same group (KIST, Korea) published the method first, then released the data:

**Tiong *et al.*, "Predicting failure progressions of structural materials via deep learning based on void topology", *Acta Materialia* 250 (2023) 118862.**
- arXiv: https://arxiv.org/abs/2205.09075
- Code: https://github.com/tiongleslie/material-failure-prediction (MIT license, TensorFlow **1.13**, which is very old)
- Method: 3D X-CT → persistent homology features → deep multimodal network → predict strain / fracture progress.
- Results: **MAE 0.09** on local strain (tensile), **MAE 0.14** on fracture progress (fatigue).

**This is the baseline any paper on this dataset must beat or compare against.**

## Why "just apply a CNN and report accuracy" is a trap

- A CNN on this data with no new question is a *method-swap* paper. Reviewers will ask
  "what did we learn that Tiong 2023 didn't show?"
- The dataset is small (276 samples total), so a plain big 3D CNN can overfit, and the
  result may be *worse* than the PH baseline.
- The way out is to ask a **new question** using this data (see file 03), not just a new model.

## Why this dataset is still a great asset

- It is **new** (published late 2025). In our searches, the only papers using it came from the group that created it.
- It has **real mechanical labels** (strain, fatigue stage), which are rare. Most CT datasets only have "defect / no defect".
- Working code for the baseline already exists, so we can reproduce it quickly.
