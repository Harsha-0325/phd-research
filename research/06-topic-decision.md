# 6. Topic Decision: Evidence, Defence and a 160-Hour Plan

> Purpose: give her a topic she can **defend**, first to her professor, then the internal doctoral committee,
> then external examiners. Every claim below has a number or a source behind it. No code yet: this is the research-planning stage.

---

## 6.1 The proposed topic

> **Machine learning for cosmic-ray muon scattering tomography: imaging dense metals where X-rays cannot reach**

One-line pitch for the professor:
*"X-ray CT can't see through thick steel containers, lead shielding or nuclear waste drums. Cosmic-ray muons can.
The imaging method exists, but the AI side of it is still basic. There's no public dataset and no review of the ML work.
I'll bring computer-science methods to it."*

---

## 6.2 Evidence the gap is real (numbers)

Paper counts from **Semantic Scholar** (free API), matching title and abstract, each topic combined with
`"deep learning" | "neural network" | "machine learning"`. Queried September 2026. **These are approximate,
because keyword search misses some papers, but the *relative* sizes are what matter.**

| Topic + ML | Papers 2020–2026 | Papers in 2025 | Reading |
|------------|------------------|----------------|---------|
| Ultrasonic testing / phased array (defects, welds) | **774** | 149 | 🔴 crowded |
| X-ray diffraction phase identification | 144 | 24 | 🔴 crowded (fast-growing, many strong groups) |
| Gamma-ray isotope identification | 128 | 34 | 🟠 competitive, national labs active |
| Weld radiography defects | 119 | 26 | 🔴 crowded (plus many unindexed low-tier papers) |
| X-ray CT defects in metals / AM | 108 | 19 | 🔴 crowded (where she was before) |
| Neutron imaging | 45 | 13 | 🟢 thin, but data is very hard to get |
| **Muon tomography / muography** | **39** | **18** | **🟢 thin *and* growing: 2 (2020) → 5 (2022) → 18 (2025)** |

Growth for muography + ML by year: 2020: 2 · 2022: 5 · 2024: 4 · **2025: 18** · 2026: 5 so far (2026 indexing lags).

**How to read this:** the field is small (you can read *all* of it) but it's accelerating. That's the ideal time to
enter. You get early citations, and nobody has written the "map of the field" yet.

### Specific gaps (as of Sept 2026, from our searches)
| # | Gap | Evidence |
|---|-----|----------|
| G1 | **No review or survey of ML in muon tomography** | alphaXiv and Semantic Scholar both return no ML-focused review. Existing reviews are about geoscience best practice (2021) or civil structures (2022), not ML |
| G2 | **No public benchmark dataset** | The newest real-data paper (DLR, Aug 2026) says data is available only "upon reasonable request" and real data "cannot be made available" |
| G3 | **ML methods are basic** | U-Nets on 2D slices, 3D CNNs, transfer learning. Trained on small simulated sets (e.g. 147 scenes) |
| G4 | **Raw muon tracks aren't used directly** | Almost all works voxelise first (PoCA), then apply a CNN. We found no point-cloud / set-model approach for imaging or material ID |
| G5 | **Sim-to-real gap is the stated central obstacle** | DLR 2026: "automated interpretation … studied almost exclusively in simulations" |

---

## 6.3 Options for the October / November deadline

| Option | What it is | Hours (of 160) | Risk | Output by end of Oct | Output by end of Nov |
|--------|-----------|----------------|------|---------------------|---------------------|
| **1. Systematic review** (fills G1) | PRISMA-style review of all ML-in-muography papers, with a taxonomy, a comparison table and open problems | ~80–100 | **Low**: no experiments | **Complete draft** | Submitted |
| **2. Benchmark paper, "Paper A"** (fills G2 + G3) | Open simulated dataset, 3 tasks, standard baselines | ~160+ | Medium: new simulator to learn | Design + first results | Technical side complete → drafting |
| **3. Both, in sequence** ⭐ | Review first (weeks 1–3), benchmark next (weeks 3–8) | 160 in Oct + Nov | Low → medium | **Review draft done** | **Benchmark technical side done** |

**Recommendation: Option 3.**
- The review is the **safe, guaranteed output for October**. It also becomes **Chapter 2 (literature review) of the thesis**
  and gives her real command of the field before any examiner questions her.
- The benchmark is the **first technical contribution**. Its design comes straight out of the review's "open problems" section, so the story is coherent.
- ⚠️ **Check with her university:** some Indian universities don't count *review* papers toward the PhD publication requirement.
  If hers doesn't, the review still pays off as a thesis chapter and a credibility boost, but the benchmark becomes the counted paper.

### Where to submit
- **Review:** *Particles* or *Instruments* (MDPI, open access, fast review; the field's own papers appear there),
  *Journal of Instrumentation (JINST)*, or *Machine Learning: Science and Technology* (IOP).
  *(Check the publication fees first. Some MDPI journals charge fees, and IOP transformative agreements or university waivers may apply.)*
- **Benchmark:** **IJCNN 2027, deadline 31 Jan 2027** (https://ijcnn.org/2027), about 39% acceptance in 2025.
  Or ICIP 2027 (deadline not yet announced). Plus an **arXiv preprint as soon as it's ready**, which is free and establishes priority.

---

## 6.4 Questions the committee will ask, and the answers

**Q1. "Your earlier work was X-ray CT of steel. Why switch to muons?"**
> It's a continuation, not a switch. Both are *tomography* (reconstructing 3D density from projections), and both image voids and
> dense inclusions in metals. X-rays fail when the object is thick or shielded (containers, lead, nuclear drums). Muons don't.
> My CNN / 3D-volume skills transfer directly. The reconstructed muon image is a 3D volume, just like CT.

**Q2. "Is this computer science or physics?"**
> The physics is handled by established, validated simulators (Geant4, used by CERN; EcoMug/CRY cosmic-ray generators).
> My contributions are CS: a systematic review, a benchmark dataset with evaluation protocols, and learning methods
> (point-set models, uncertainty, domain adaptation).

**Q3. "You have no real data. Isn't this just simulation?"**
> Simulation-first is the norm in this field. The latest paper validated on real cargo scans (DLR, 2026) trained *only* on simulation.
> We'll replicate published detector geometries to stay realistic. For real data, we can approach Indian groups
> (Saha Institute of Nuclear Physics, Kolkata, which has muon tomography work and a 2022 HBNI PhD on it).

**Q4. "Where is the novelty?"**
> G1–G4 in section 6.2. As of Sept 2026: no ML review, no public benchmark, no raw-track (point-set) learning.

**Q5. "Why does this matter for India?"**
> Nuclear waste management (Department of Atomic Energy programmes), port and border security, and inspection of ageing bridges
> (corroded steel rebar inside concrete). India also has muon expertise: the GRAPES-3 muon telescope (TIFR, Ooty) and SINP Kolkata.

**Q6. "Can you finish this with your resources?"**
> Yes. The review needs no compute. The simulation runs on CPU and parallelises easily. Training fits on a single GPU.
> All tools are free and open-source.

**Q7. "Will you use LLMs / GenAI?"**
> Not as the core method. It isn't needed, and forcing it in would weaken the paper. (Optional: an LLM can help *screen* abstracts
> during the systematic review, but it must be declared in the methods section and checked by hand.)

---

## 6.5 The 160-hour plan (4 weeks × 40 h), research first

### Week 1 (40 h): lock the topic and build the evidence base
- [ ] Present this document to the professor → **get a go / no-go** (gate)
- [ ] Write the review protocol: research questions, databases (Semantic Scholar, arXiv, Scopus via the university library, IEEE Xplore), search strings, inclusion and exclusion criteria
- [ ] Run the searches and export everything into one spreadsheet (expect ~60–120 hits → ~40–60 included)
- [ ] Read the 8 key papers from file 05 in full, and take notes on method, data, task, metrics and limitations

### Week 2 (40 h): screening and extraction
- [ ] Screen titles and abstracts, then full texts. Log PRISMA counts (how many found, screened, excluded, and why)
- [ ] Data-extraction sheet per paper: task (imaging, material ID, anomaly, denoising, momentum estimate), input representation (raw tracks, PoCA voxels, 2D slices), model, data source (simulated vs. real), simulator, metrics, code or data availability
- [ ] Draft the **taxonomy figure** (task × representation × model family)

### Week 3 (40 h): write the review, design the benchmark
- [ ] Write the review: intro → background (muon physics in one page) → method → taxonomy → comparison tables → **open problems** → conclusion
- [ ] From the open problems, write the **benchmark design doc**: tasks, scene types, simulator choice, dataset sizes, splits, metrics, baselines
- [ ] Choose the simulator after trying the options: TomOpt / muograph (Python, fast) vs. Geant4 + EcoMug (standard, slower)

### Week 4 (40 h): finish the review, start the benchmark
- [ ] Review draft complete → to the professor
- [ ] Generate the first small dataset and run the first baseline (PoCA + threshold, then a 3D CNN)
- [ ] Update the benchmark plan with what was learned

### November: benchmark technical side
- Full dataset → all baselines → results tables and figures → **technical side complete by end of November** → draft for IJCNN (31 Jan 2027)

---

## 6.6 What we still need to find out (open questions)
1. Does her university count **review papers** toward the PhD requirement? Is **Scopus/SCI indexing** required?
2. Is her professor comfortable supervising a physics-adjacent topic? (The pitch in 6.1 plus Q1–Q2 is meant to address this.)
3. Is there any contact at SINP Kolkata, TIFR or BARC for later real-data collaboration? (This is optional, not needed for October.)

## Sources for this file
- Semantic Scholar API (paper counts): https://api.semanticscholar.org
- DLR maritime MST anomaly detection, 2026: https://www.alphaxiv.org/abs/2608.12068
- GRAPES-3 (TIFR): https://www.tifr.res.in/grapes3/
- Muography for inspection of civil structures (review, 2022): https://www.mdpi.com/2410-390X/6/4/77
- Muon tomography in geoscience, best-practice guide (2021): https://www.sciencedirect.com/science/article/pii/S0012825221003433
- Muon scattering tomography for nuclear waste storage (CHEP 2025): https://www.epj-conferences.org/articles/epjconf/abs/2025/22/epjconf_chep2025_01123/epjconf_chep2025_01123.html
- Understanding muon scattering using Geant4 (Indian symposium proceedings): https://sympnp.org/proceedings/61/G70.pdf
- IJCNN 2027 call for papers: https://ijcnn.org/2027
