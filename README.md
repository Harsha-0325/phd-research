# PhD Research: Deep Learning for X-ray CT of Metals

A shared workspace for finding a research gap and turning it into two publishable papers.

**Starting point:** a public X-ray CT dataset of deformed ferritic steel
([Lee et al., *Scientific Data*, 2025](https://www.nature.com/articles/s41597-025-06141-y)).
**Goal:** find where deep-learning / computer-science skills can make a *real* contribution
in the "imaging + metals" space, not just another accuracy table.

## ⭐ Start here: [`research/05-cross-domain-scan.md`](research/05-cross-domain-scan.md)

The latest recommendation is **deep learning for muon scattering tomography**: imaging dense metals with cosmic rays.
It's an emerging field with basic ML, no public benchmark, and a direct fit for CNN / 3D-volume skills.
Files 01–03 below were the first pass, anchored on the steel CT dataset. Keep them as background only.

## Earlier files (background)

| # | File | What it tells you | Time to read |
|---|------|-------------------|--------------|
| 1 | [`research/01-reference-dataset.md`](research/01-reference-dataset.md) | What the steel CT dataset is, and what has already been done with it | 5 min |
| 2 | [`research/02-landscape.md`](research/02-landscape.md) | Map of the field: which topics are crowded, which are thin | 10 min |
| 3 | [`research/03-gap-and-paper-plan.md`](research/03-gap-and-paper-plan.md) | **The recommendation:** two paper ideas, why they are gaps, how to do them | 10 min |
| 4 | [`research/04-venues-and-competition.md`](research/04-venues-and-competition.md) | Acceptance rates, how competitive it is, most recent papers | 5 min |
| 5 | [`research/glossary.md`](research/glossary.md) | Plain-English meanings of the materials-science words | as needed |

If you only read one file, read **#3**.

## Status

- [x] Literature scan across ~20 sub-areas (X-ray CT, radiography, neutron imaging, batteries, corrosion, fatigue, anomaly detection, foundation models)
- [x] Gap analysis and two-paper plan
- [ ] Download the dataset and confirm exactly what files it contains
- [ ] Reproduce the existing baseline (persistent homology + deep learning) in PyTorch
- [ ] Paper 1 experiments
- [ ] Paper 2 benchmark design

## Important caveat

The gap claims here come from web searches (September 2026), not a full systematic review.
Before writing a paper, **re-check each gap on Google Scholar / Scopus** and read the key
papers linked in each file. "I didn't find it" is not the same as "it doesn't exist".
