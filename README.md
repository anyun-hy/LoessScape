# LoessScape

**A Continuous-Region Land-Cover Benchmark for Semantic Segmentation under Spatially Clustered Imbalance**

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[![Dataset on Zenodo](https://img.shields.io/badge/Dataset-Zenodo-blue.svg)](https://doi.org/10.5281/zenodo.20340667)
[![Paper (preprint)](https://img.shields.io/badge/Paper-preprint-green.svg)](paper/LoessScape_preprint.pdf)

LoessScape is a pixel-level semantic segmentation benchmark built entirely under a **continuous-region survey paradigm**. Instead of curating geographically isolated tiles, it preserves the complete spatial organization of a representative Loess Plateau region (~1,853 km²) through a semantic-content-aware stratified partitioning strategy. This design explicitly exposes the challenge of **Spatially Clustered Imbalance**, in which geometrically thin minority classes are persistently embedded within strongly autocorrelated dominant terrains.

---

## Highlights

- **Continuous-region paradigm** — spatial continuity and structural complexity of complete geographic entities are preserved, rather than disrupted by isolated sampling.
- **Spatially Clustered Imbalance** — a realistic challenge where thin minority classes are siloed inside dominant, spatially autocorrelated terrains.
- **Comprehensive benchmark** — hierarchical supervised segmentation on Level-1 / Level-2 tasks plus unsupervised domain adaptation under spatial distribution shift.
- **Cross-disciplinary diagnostics** — a landscape-ecology-based framework that identifies the counterintuitive **Landscape-Error Paradox** and characterizes **Spatial Siege**.

---

## Dataset Access

The full dataset (~9.7 GB) is archived on **Zenodo**:

> **DOI:** [10.5281/zenodo.20340667](https://doi.org/10.5281/zenodo.20340667)

| Property | Value |
|:---|:---|
| Region | Representative Loess Plateau region (~1,853 km²) |
| Native Resolution | 2.0 m/pixel |
| Tile Size | 512 × 512 pixels |
| Total Tiles | 9,888 (3 scales) |
| Label Classes | 14 (Level-2) / 7 (Level-1) |
| Split Ratio | Train 70% / Val 15% / Test 15% |
| License | CC BY-NC-SA 4.0 |

### Multi-Scale Design

All tiles are output as 512×512 pixels, but each scale reads a different-sized window from the source image — changing the geographic field of view, not just resizing.

| Scale | GSD | Coverage | Role |
|:---:|:---:|:---:|:---|
| `scale_1_0.5` | 1.0 m | 512 m | Micro-Detail — fine textures and edges |
| `scale_1_1` | 2.0 m | 1024 m | Baseline — native resolution reference |
| `scale_1_2` | 4.0 m | 2048 m | Macro-Context — broader spatial context |

All three scales share the same upper-left anchor point, enabling cross-scale tile pairing.

### Tile Counts

| Scale | Train | Val | Test | Total |
|:---:|:---:|:---:|:---:|:---:|
| `scale_1_0.5` | 2,265 | 481 | 490 | 3,236 |
| `scale_1_1` | 2,321 | 493 | 497 | 3,311 |
| `scale_1_2` | 2,335 | 503 | 503 | 3,341 |
| **All** | **6,921** | **1,477** | **1,490** | **9,888** |

### Class Taxonomy

Two-level hierarchy based on the China national standard GB/T 21010-2017 — 14 Level-2 classes grouped into 7 Level-1 categories: Cropland, Orchard, Forest, Grassland, Built-up, Transportation, Water. `NoData = 255` (outside the study-area boundary; use as `ignore_index` during training).

Full class definitions, color palette, and per-tile metadata format are documented in the dataset's own `README.md` and `metadata/class_info.json`.

---

## Repository Layout

```text
LoessScape/
├── paper/
│   └── LoessScape_preprint.pdf   # Compiled manuscript (preprint)
├── README.md                     # This page
├── CITATION.cff                  # Machine-readable citation metadata
└── LICENSE                       # CC BY-NC-SA 4.0
```

> The dataset tiles themselves are **not** hosted on GitHub — download them from Zenodo (link above).

---

## Paper

**LoessScape: A Continuous-Region Land-Cover Benchmark for Semantic Segmentation under Spatially Clustered Imbalance**

A preprint of the manuscript is available at [`paper/LoessScape_preprint.pdf`](paper/LoessScape_preprint.pdf).

> **Abstract.** Existing remote-sensing semantic segmentation datasets are predominantly constructed under a scene-centric paradigm. By curating geographically isolated tiles, this paradigm disrupts spatial continuity and weakens the structural complexity of complete geographic entities. As a result, models evaluated on such idealized benchmarks often experience marked performance degradation when deployed in continuous real-world landscapes. To address this limitation, we introduce LoessScape, a semantic segmentation benchmark built entirely under a continuous-region survey paradigm. Instead of isolated sampling, the dataset preserves the complete spatial organization of a Loess Plateau region through a semantic-content-aware stratified partitioning strategy. This design explicitly exposes the challenge of Spatially Clustered Imbalance, in which geometrically thin minority classes are persistently embedded within strongly autocorrelated dominant terrains. Based on this dataset, we establish a comprehensive benchmark spanning hierarchical supervised segmentation on the L1 and L2 tasks and unsupervised domain adaptation under spatial distribution shift. Beyond aggregate empirical metrics, our cross-disciplinary diagnostic framework draws on landscape ecology to analyze the underlying failure patterns. Specifically, we identify a counterintuitive Landscape-Error Paradox and use spatial statistical analysis to characterize the phenomenon of Spatial Siege, showing that segmentation difficulty extends beyond localized boundary confusion into broader contextual erosion.

---

## Citation

If you use LoessScape in your research, please cite both the paper and the dataset.

**Paper:**

```bibtex
@article{wang2026loessscape,
  title   = {LoessScape: A Continuous-Region Land-Cover Benchmark for Semantic Segmentation under Spatially Clustered Imbalance},
  author  = {Wang, Junjie and Jiang, Ping and Liu, Gang and Liu, Hanye and Xu, Lihui and Liu, Sijun and Lei, Xin},
  year    = {2026},
  note    = {Preprint}
}
```

**Dataset:**

```bibtex
@dataset{loessscape2026dataset,
  title     = {LoessScape: A Multi-Scale Semantic Segmentation Dataset for Loess Plateau Land Use},
  author    = {Wang, Junjie and Jiang, Ping and Liu, Gang and Liu, Hanye and Xu, Lihui and Liu, Sijun and Lei, Xin},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20340667},
  note      = {Licensed under CC BY-NC-SA 4.0}
}
```

---

## License

This repository and the LoessScape dataset are released under the
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/) license.

---

## Contact

For questions about LoessScape, please contact the first author **Junjie Wang** — `jj_wang@stu.xidian.edu.cn`
School of Computer Science and Technology, Xidian University, Xi'an, Shaanxi, China
