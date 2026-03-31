# rootseg-ct — Automated X-ray CT Segmentation Pipeline for *Arabidopsis thaliana* Roots and Root Hairs

This repository contains the Python notebooks developed for the automated segmentation of *Arabidopsis thaliana* roots and root hairs from high-resolution X-ray computed tomography (CT) image stacks. The pipeline was benchmarked against VGSTUDIO MAX, a commercial CT analysis tool, across six datasets spanning three genotypes with contrasting root hair densities.

The code accompanies the following publication:

> Kozhuharova B, Heitauer M, Kardjilov N, Manke I, Sauer M, Tötzke C, Nowak J. **Automated python-based segmentation pipeline for roots and root hairs in X-ray CT scans: An alternative to manual VGSTUDIO MAX segmentation.** *Plant Methods* (in preparation). DOI: to be added upon publication.

The associated dataset (CT image stacks, segmentation masks, gray-value histograms) is available at the Helmholtz-Zentrum Berlin (HZB) data repository: DOI to be added upon publication.

---

## Repository Contents

| Notebook | Description |
|---|---|
| `segmentation_pipeline.ipynb` | Core segmentation pipeline: NLM denoising, min-max intensity normalisation, sand mask generation, pixel-wise classification of root/air/other voxels, connected-component labelling, and connectivity-based 3D root tracking across slices |
| `create_binary.ipynb` | Converts grayscale TIFF stacks (e.g. from VGSTUDIO MAX exports) into binary segmentation masks by thresholding pixel intensities |
| `concatenate_stacks.ipynb` | Reassembles batch-processed sub-stacks into a single continuous volume, outputting individually numbered 2D TIFF slices with zero-padded filenames |
| `create_overlay.ipynb` | Generates colour-coded voxel-wise overlay images comparing two segmentation volumes: true positives (white), false positives (red), and false negatives (blue) |
| `quantitative_evaluation.ipynb` | Computes standard binary segmentation metrics — Dice Similarity Coefficient (DSC), True Positive Rate (TPR), False Negative Rate (FNR), and False Positive Rate (FPR) — by comparing pipeline output against a ground-truth segmentation |
| `create_histogram.ipynb` | Loads gray-value histogram data exported from VGSTUDIO MAX after NLM denoising and produces publication-ready plots of intensity distributions with per-class overlays (root, sand, background) |
| `overlap_gray_values.ipynb` | Quantifies background signal contamination within the dominant intensity ranges of root and sand classes across multiple datasets, as a function of cumulative probability mass coverage |
| `barplot.ipynb` | Produces a publication-ready grouped bar plot comparing DSC and TPR across all datasets, with a mean line and ± standard deviation band |

---

## Requirements

The notebooks were developed and tested with **Python 3.12.4** and require the following packages:

```
numpy==2.2.5
imageio==2.37.0
scipy==1.15.3
matplotlib==3.10.0
pandas==2.3.1
scikit-image==0.25.0
natsort==8.4.0
tifffile==2025.2.18
```

Install all dependencies with:

```bash
pip install numpy==2.2.5 imageio==2.37.0 scipy==1.15.3 matplotlib==3.10.0 pandas==2.3.1 scikit-image==0.25.0 natsort==8.4.0 tifffile==2025.2.18
```

---

## Usage

1. Clone the repository:
```bash
git clone https://github.com/[USERNAME]/rootseg-ct.git
cd rootseg-ct
```

2. Open the notebooks in Jupyter:
```bash
jupyter notebook
```

3. **Update file paths** in each notebook to point to your local data directories. All notebooks currently contain example paths that must be replaced before running.

4. Run the notebooks in the following recommended order:
   1. `segmentation_pipeline.ipynb` — generate segmentation masks
   2. `create_binary.ipynb` — convert outputs to binary masks
   3. `concatenate_stacks.ipynb` — reassemble batch outputs into full volumes
   4. `create_overlay.ipynb` — visualise agreement between segmentations
   5. `quantitative_evaluation.ipynb` — compute performance metrics
   6. `create_histogram.ipynb` — plot gray-value distributions
   7. `overlap_gray_values.ipynb` — analyse background overlap
   8. `barplot.ipynb` — generate summary performance plots

---

## Data

The full dataset used in this study — including the cropped reconstructed CT image stacks (16-bit TIFF), VGSTUDIO MAX ground-truth segmentation masks, Python pipeline segmentation masks, gray-value histograms (extracted after NLM denoising), and the full gray-value distributions of all volumes — is publicly available at:

> HZB Data Repository: https://doi.org/10.5442/ND000018

Note: CT image stacks in the repository are cropped versions of the original raw volumes, reduced to retain only the root-containing region for storage efficiency.

---

## Citation

If you use this code in your research, please cite:

```
Kozhuharova B, Heitauer M, Kardjilov N, Manke I, Sauer M, Tötzke C, Nowak J.
Automated python-based segmentation pipeline for roots and root hairs in X-ray CT scans:
An alternative to manual VGSTUDIO MAX segmentation.
Plant Methods (in preparation). DOI: to be added.
```

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Contact

For questions regarding the code, please contact:  
**Jacqueline Nowak** — janowak@uni-potsdam.de  
**Boyana Kozhuharova** — boyana.kozhuharova.1@uni-potsdam.de  
**Magdalena Heitauer** — magdalena.heitauer@uni-potsdam.de
