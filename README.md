# LoessScape

### A Continuous-Region Land-Cover Benchmark for Semantic Segmentation under Spatially Clustered Imbalance

[![Dataset on Zenodo](https://img.shields.io/badge/Dataset-Zenodo%20%7C%2010.5281%2Fzenodo.20340667-1682D4.svg)](https://doi.org/10.5281/zenodo.20340667)
[![Paper](https://img.shields.io/badge/Paper-Preprint%20(PDF)-2E7D32.svg)](paper/LoessScape_preprint.pdf)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

**LoessScape** is a pixel-level semantic segmentation benchmark for land use / land cover (LULC)
mapping, built entirely under a **continuous-region survey paradigm**. Instead of curating
geographically isolated tiles, it preserves the complete spatial organization of a representative
Loess Plateau region (~1,853 km²), explicitly exposing the challenge of **Spatially Clustered
Imbalance** — geometrically thin minority classes persistently embedded within strongly
autocorrelated dominant terrains.

---

## Quick Links

| | |
|:--|:--|
| **Download the dataset** | [Zenodo · 10.5281/zenodo.20340667](https://doi.org/10.5281/zenodo.20340667) |
| **Read the paper** | [Preprint PDF](paper/LoessScape_preprint.pdf) |
| **Cite** | [Citation section](#citation) |
| **License** | CC BY-NC-SA 4.0 (non-commercial academic use) |

---

## Download

The full dataset (~9.7 GB, **9,888 tiles**) is archived on **Zenodo**:

### → https://doi.org/10.5281/zenodo.20340667

| File | Contents |
|:--|:--|
| `images.zip` | Multi-scale RGB GeoTIFF tiles (3 scales × train/val/test) |
| `masks.zip` | Pixel-level semantic mask tiles (same structure) |
| `metadata.zip` | `class_info.json`, `dataset_info.json`, per-split `*_info.json` |
| `README.md` | Full dataset documentation |
| `LICENSE` | CC BY-NC-SA 4.0 |
| `MD5SUMS.txt` | Checksums for integrity verification |

After download, unzip `images.zip`, `masks.zip` and `metadata.zip` into a common root to
reconstruct the dataset directory tree (see [Directory Structure](#directory-structure)).

---

## Paper

**LoessScape: A Continuous-Region Land-Cover Benchmark for Semantic Segmentation under
Spatially Clustered Imbalance**

A preprint of the manuscript is available here: **[paper/LoessScape_preprint.pdf](paper/LoessScape_preprint.pdf)**

<details>
<summary><b>Abstract</b></summary>

Existing remote-sensing semantic segmentation datasets are predominantly constructed under a
scene-centric paradigm. By curating geographically isolated tiles, this paradigm disrupts spatial
continuity and weakens the structural complexity of complete geographic entities. As a result,
models evaluated on such idealized benchmarks often experience marked performance degradation when
deployed in continuous real-world landscapes. To address this limitation, we introduce LoessScape,
a semantic segmentation benchmark built entirely under a continuous-region survey paradigm. Instead
of isolated sampling, the dataset preserves the complete spatial organization of a Loess Plateau
region through a semantic-content-aware stratified partitioning strategy. This design explicitly
exposes the challenge of Spatially Clustered Imbalance, in which geometrically thin minority classes
are persistently embedded within strongly autocorrelated dominant terrains. Based on this dataset,
we establish a comprehensive benchmark spanning hierarchical supervised segmentation on the L1 and
L2 tasks and unsupervised domain adaptation under spatial distribution shift. Beyond aggregate
empirical metrics, our cross-disciplinary diagnostic framework draws on landscape ecology to analyze
the underlying failure patterns. Specifically, we identify a counterintuitive Landscape-Error
Paradox and use spatial statistical analysis to characterize the phenomenon of Spatial Siege,
showing that segmentation difficulty extends beyond localized boundary confusion into broader
contextual erosion.

</details>

---

## Highlights

- **Continuous-region paradigm** — spatial continuity and the structural complexity of complete
  geographic entities are preserved, rather than disrupted by isolated sampling.
- **Spatially Clustered Imbalance** — a realistic challenge in which thin minority classes are
  siloed inside dominant, spatially autocorrelated terrains.
- **Comprehensive benchmark** — hierarchical supervised segmentation on Level-1 / Level-2 tasks,
  plus unsupervised domain adaptation under spatial distribution shift.
- **Cross-disciplinary diagnostics** — a landscape-ecology-based framework that identifies the
  counterintuitive **Landscape-Error Paradox** and characterizes **Spatial Siege**.

---

## Dataset at a Glance

| Property | Value |
|:--|:--|
| Region | Representative Loess Plateau region (~1,853 km²) |
| Native resolution | 2.0 m/pixel |
| Tile size | 512 × 512 pixels |
| Overlap ratio | 25% (128 px) |
| Total tiles | 9,888 (across 3 scales) |
| Label classes | 14 (Level-2) / 7 (Level-1) |
| Split ratio | Train 70% / Val 15% / Test 15% |
| Annotation | Manually delineated pixel-level semantic masks |
| License | CC BY-NC-SA 4.0 |

### Multi-Scale Design

All tiles are output as 512 × 512 pixels, but each scale reads a different-sized window from the
source image — changing the geographic field of view, not simply resizing the output. The three
scales share the **same upper-left anchor point**, enabling cross-scale tile pairing.

| Scale | GSD | Coverage | Role |
|:-:|:-:|:-:|:--|
| `scale_1_0.5` | 1.0 m | 512 m | Micro-Detail — fine textures and edges |
| `scale_1_1` | 2.0 m | 1024 m | Baseline — native resolution reference |
| `scale_1_2` | 4.0 m | 2048 m | Macro-Context — broader spatial context |

### Tile Counts

| Scale | Train | Val | Test | Total |
|:-:|:-:|:-:|:-:|:-:|
| `scale_1_0.5` | 2,265 | 481 | 490 | 3,236 |
| `scale_1_1` | 2,321 | 493 | 497 | 3,311 |
| `scale_1_2` | 2,335 | 503 | 503 | 3,341 |
| **All** | **6,921** | **1,477** | **1,490** | **9,888** |

---

## Class Taxonomy

A two-level hierarchy based on the China national standard **GB/T 21010-2017** — 14 Level-2
classes grouped into 7 Level-1 categories:

| Level-1 | Level-2 (code — name) |
|:--|:--|
| Cropland | 12 — Irrigated Land · 13 — Dryland |
| Orchard | 21 — Orchard |
| Forest | 31 — Arbor Forest · 32 — Shrubland · 33 — Other Forest |
| Grassland | 43 — Other Grassland |
| Built-up | 51 — Urban · 52 — Rural · 53 — Disturbed Land · 54 — Other Built-up |
| Transportation | 61 — Rural Road · 62 — Other Transportation |
| Water | 71 — Rivers/Lakes/Ponds |

`NoData = 255` marks areas outside the study-area boundary — set it as `ignore_index` during
training. Full class definitions, the color palette, and the per-tile metadata format are
documented in the dataset's bundled `README.md` and `metadata/class_info.json`.

---

## Directory Structure

After unzipping the archives into a common root:

```text
LoessScape/
├── images/                       # Multi-scale RGB tiles (GeoTIFF)
│   ├── scale_1_0.5/{train,val,test}/
│   ├── scale_1_1/{train,val,test}/
│   └── scale_1_2/{train,val,test}/
├── masks/                        # Pixel-level semantic masks (same structure)
│   ├── scale_1_0.5/{train,val,test}/
│   ├── scale_1_1/{train,val,test}/
│   └── scale_1_2/{train,val,test}/
├── metadata/
│   ├── class_info.json           # Class hierarchy, color palette, remapping
│   ├── dataset_info.json         # Dataset-level summary and statistics
│   └── {train,val,test}_info.json  # Per-tile metadata for each split
├── README.md
└── LICENSE
```

Tile file name: `{scale}_{split}_{row}_{col}_{tileID}.tif` — e.g. `scale_1_1_train_5376_8064_6784.tif`.

---

## Citation

If you use **LoessScape** in your research, please cite both the paper and the dataset.

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
@dataset{wang2026loessscape_data,
  title     = {LoessScape: A Multi-Scale Semantic Segmentation Dataset for Loess Plateau Land Use},
  author    = {Wang, Junjie and Jiang, Ping and Liu, Gang and Liu, Hanye and Xu, Lihui and Liu, Sijun and Lei, Xin},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.20340667},
  url       = {https://doi.org/10.5281/zenodo.20340667},
  note      = {Licensed under CC BY-NC-SA 4.0}
}
```

---

## License

LoessScape is released under the
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
license — free for non-commercial academic research, with attribution. The underlying base imagery
is derived from Google Earth imagery and remains subject to the
[Google Maps / Google Earth Terms of Service](https://www.google.com/help/terms_maps/).

---

## Contact

For questions about LoessScape, please contact the first author **Junjie Wang** —
`jj_wang@stu.xidian.edu.cn`
School of Computer Science and Technology, Xidian University, Xi'an, Shaanxi, China
