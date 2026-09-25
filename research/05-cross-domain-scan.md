# 5. Cross-Domain Scan: Beyond the Steel CT Dataset

> **Why this file exists:** the earlier plan (file 03) still leaned on the steel X-CT dataset. That direction has
> already been tried and it didn't land. This file starts fresh. It keeps only her **skills**
> (CNNs, deep learning on images, volumes and signals) and asks: *which neighbouring areas, using other
> radiation, other sensing methods or other metal-like materials, have a real research gap?*

## The grid we scanned

| Area | Signal / modality | Material link | Crowdedness | Public data | Verdict |
|------|------------------|---------------|-------------|-------------|---------|
| X-ray diffraction (XRD) phase ID | X-ray, 1D pattern | alloys, crystals | 🔴 many DL papers (npj Comput. Mater. 2025, Nat. Sci. Rev. 2025, arXiv 2026 tools) | Yes (simulated) | Skip |
| X-ray CT pores in 3D-printed metal | X-ray, 3D | metals | 🔴 | Yes | Skip |
| Weld / casting radiography | X-ray, 2D | metals | 🔴 | Yes | Skip |
| Solder-joint voids in chip packaging | X-ray, 2D/3D | solder metals | 🟠 applied CV | **No, proprietary** | Skip (no data) |
| Metal scrap sorting (LIBS, dual-energy X-ray) | spectra + images | Al, steel scrap | 🟠 | **Mostly proprietary** | Skip (no data) |
| Keyhole pores seen with synchrotron X-ray | high-speed X-ray video | Ti, steel | 🟠 top groups (*Science* 2023, Argonne) | Rare | Skip (needs synchrotron) |
| Gamma-ray isotope identification | gamma spectra, 1D | radioactive metals | 🟠 CNNs since 2019; national labs active (transfer learning 2024, domain adaptation 2026) | Simulated | Possible, but competitive |
| Ultrasonic phased-array NDT | ultrasound B-scans | welds, steel | 🟠 | Scarce, **no unified benchmark** | Backup option |
| Neutron imaging | neutrons | hydrogen in metals | 🟢 thin | Very hard to get | Future work |
| **Muon scattering tomography (muography)** | **cosmic-ray muons, 3D** | **high-Z metals (uranium, lead, steel), steel rebar in concrete, nuclear waste** | **🟢→🟠 emerging: about 10–15 ML papers in 2025–26, mostly from physics groups** | **No public dataset; open-source simulators exist** | **⭐ Recommended** |

## ⭐ Recommendation: deep learning for muon scattering tomography

### What it is, in one paragraph (no physics degree needed)
Cosmic rays create **muons**, heavy cousins of electrons that rain down everywhere, roughly one per cm² per minute.
They pass through metres of steel and concrete. When a muon passes near **heavy (high-Z) material** such as uranium,
lead or steel, it gets deflected more. Put detectors above and below an object, measure each muon's path in and out,
and the **pattern of deflections forms a 3D image of the dense material inside**. It's like CT, but it's passive
(no X-ray source) and it sees through things X-rays can't. The one equation that matters: deflection width grows as the material gets
denser or heavier.

**Uses:** scanning shipping containers for nuclear material or weapons, inspecting **nuclear waste barrels**, finding
**corroded steel rebar inside concrete** bridges, imaging volcanoes and pyramids.

### Why it's a gap for a CS / DL person
1. **The ML is still basic.** The newest real-data paper (German Aerospace Center, Aug 2026, arXiv 2608.12068) uses an
   attention U-Net on **2D slices** plus a hand-crafted score, trained on **147 simulated scenes**.
   Others use 3D CNNs, U-Net denoising and transfer learning. Modern CS tools (point-cloud / set transformers, diffusion
   models, calibrated uncertainty, self-supervised pre-training) are **largely absent**.
2. **The authors list the gaps themselves:**
   - "automated interpretation of MST volumes has so far been studied almost exclusively in simulations"
   - they work on 2D slices "at the cost of depth resolution"
   - they have "no access to raw detector hits"
   - their data is available "upon reasonable request" only, and the real data "cannot be made available"
3. **No public benchmark dataset.** That's the same kind of gap we found for industrial CT, but in a field that's
   *growing fast* (a steady stream of arXiv papers through 2026) and hasn't been claimed by CS researchers yet.
4. **Muon data is naturally a point set.** Each muon is one "point" (entry, exit, deflection angle). Today almost everyone
   first bins muons into a voxel grid (a method called PoCA) and then runs a CNN. Learning **directly from raw muon tracks** with
   PointNet / set transformers is, in our searches, **not done yet** for imaging or material ID.
5. **Her skills transfer directly.** The reconstructed output is a 3D density volume, the same data shape as the
   CT volumes she already knows how to handle.

### Candidate papers
**Paper A: open benchmark and baselines ("MuonBench").**
- Simulate a public dataset with open tools. Scenes: containers, waste barrels, rebar in concrete. Tasks: material classification (low/mid/high-Z),
  anomaly detection (benign vs. hidden high-Z object), and short-exposure denoising (few muons → good image).
- Run the standard baselines on it: PoCA+CNN, U-Net, 3D CNN, reconstruction-based anomaly detection.
- Why it gets accepted: the field explicitly lacks shared data, and benchmarks get cited.
- Venues: **NeurIPS Datasets & Benchmarks**, *JINST*, *NIM A*, *Particles*, the Muographers conference.

**Paper B: learning from raw muon tracks.**
- Use point-cloud / set-transformer models that take individual muon tracks directly (no voxel binning).
- Main claim to test: **the same accuracy with far fewer muons**. Fewer muons means shorter scans, and scan time is the biggest practical bottleneck.
- Add calibrated uncertainty (conformal prediction), so a security officer gets "uranium with 95% confidence", not just a label.
- Venues: WACV / BMVC / ICIP, or the NeurIPS **ML4PS** (Machine Learning and the Physical Sciences) workshop for early feedback, then a journal.

Paper A creates the data; Paper B uses it. Together they form a coherent thesis:
> **"Learning from sparse cosmic-ray muon data for non-destructive inspection of dense materials"**

### Tools that exist (so we don't start from zero)
- **Geant4**: the standard particle-physics simulator (open source, C++, heavy but reliable)
- **EcoMug**: a fast cosmic-muon generator used with Geant4
- **muograph**: Python library for muon scattering analysis (`pip install`), https://github.com/MaximeLagrange/muograph
- **TomOpt**: differentiable, PyTorch-style muon tomography simulation (fast and Python-friendly)
- Example Geant4 + ML repos on GitHub (e.g. muon-tomography-ML-id)

### Honest risks
- **New domain.** She'll need about 2–3 weeks to learn the basics: what a muon is, the PoCA algorithm and how the simulator works. Mitigation: start with
  TomOpt / muograph (pure Python), not raw Geant4.
- **Simulation only.** Real muon data is rarely public, so Paper A will be simulation-based. That's normal in this field
  (the German Aerospace Center paper also trained only on simulation), but reviewers will ask about realism. Mitigation: match published detector setups.
- **Physics reviewers.** Journals in this field will check the physics. Mitigation: keep claims about the ML, and cite the physics carefully.
- **Compute:** simulation is CPU-heavy but parallelises easily. Training fits on her GPU.

### Key papers to read first (in this order)
1. From Simulation to Real Scans: Anomaly Detection in Maritime Cargo with MST (Aug 2026): https://www.alphaxiv.org/abs/2608.12068
2. Transfer learning for material Z classification with muon tomography (2025): https://www.alphaxiv.org/abs/2504.12305
3. Muon-scattering material ID with momentum encoding and unsupervised domain adaptation (Jun 2026): https://www.alphaxiv.org/abs/2606.30028
4. U-Net image enhancement for short-time MST (Feb 2026): https://www.alphaxiv.org/abs/2602.07060
5. Gradient-descent reconstruction for muon tomography in PyTorch (Nov 2025): https://www.alphaxiv.org/abs/2511.05226
6. Nuisance-aware muon tomography (Jun 2026): https://www.alphaxiv.org/abs/2606.20180
7. Structural defect detection in concrete with muon tomography, 3D CNN (Apr 2026): https://www.alphaxiv.org/abs/2604.03741
8. Structural diagnostics with muon tomography and deep learning (INFN/CERN, 2025): https://www.alphaxiv.org/abs/2502.03339

## Backup directions (if muography doesn't click with her)
- **Ultrasonic phased-array NDT of welds.** Data is scarce and methods don't generalise across scanners. A cross-scanner benchmark would be a gap.
  Refs: https://pmc.ncbi.nlm.nih.gov/articles/PMC12527071/ · https://arxiv.org/pdf/2112.06650
- **Gamma-ray isotope identification.** Moderate competition. A 2025 systematic review explicitly calls for "standardized datasets
  and physics-informed ML". Refs: [Galib 2021](https://consensus.app/papers/details/956c3ca0e73e5fad80cc0d7b35240c00/),
  [NaI(Tl) ML review 2025](https://consensus.app/papers/details/2fdda077be355d1fa18db102673e8352/),
  [PNNL transfer learning 2024](https://www.alphaxiv.org/abs/2412.07069), [Domain adaptation 2026](https://www.alphaxiv.org/abs/2603.05719)
- **Volumetric anomaly detection benchmark for industrial CT** (from file 03). This idea still stands and does **not** depend on the steel dataset.
