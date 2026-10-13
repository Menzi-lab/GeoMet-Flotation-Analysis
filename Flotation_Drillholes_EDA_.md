# GeoMet Flotation Data: Cu, Fe and S vs Flotation Performance

## Overview
This notebook explores whether Cu, Fe and S head assays are associated with rougher flotation variables (`fr`, `xr`) and locked-cycle test copper recovery (`LCT`). It also provides an optional nearest-neighbour join to drillhole assays.

A key distinction: **`fr` is the mass fraction of feed reporting to rougher concentrate, not a recovery.** The implied rougher Cu recovery calculation assumes `xr` is rougher-concentrate Cu grade; verify that definition against the source paper before relying on the calculation.

## Dataset and setup
The notebook was prepared around the GeoMet dataset hosted on Zenodo:
- https://zenodo.org/records/7051975

Create a `data/` folder and place the downloaded `flotation.csv` there. To run the drillhole integration section, also place `drillholes.csv` in `data/`, if available and permitted by the dataset's licence/terms.

Expected structure:
```text
geomet-flotation-drillholes-eda/
├── Flotation_Drillholes_EDA_GitHub_Ready.ipynb
├── README.md
├── requirements.txt
├── data/
│   ├── flotation.csv       # obtain from source; not included here
│   └── drillholes.csv      # optional; obtain from source; not included here
└── figures/                # generated when notebook runs
```

## Run locally
Use Python 3.10 or newer. In a terminal:

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
jupyter lab
```

Open the notebook and choose **Restart Kernel and Run All Cells**. The notebook raises a clear error if `flotation.csv` is missing. Drillhole matching is optional and will be skipped if `drillholes.csv` is not present.

## Methods
- Data-quality and missingness checks
- Assay conversion from ppm to wt%
- Descriptive statistics and distributions
- Pearson and Spearman correlations
- Benjamini–Hochberg false-discovery-rate adjustment for the main exploratory tests
- A mass-balance consistency check for implied rougher copper recovery
- Hole-level sensitivity analysis
- Optional nearest-neighbour drillhole assay matching in 3D, with match distance and unmatched samples retained
- Exploratory correlations with drillhole variables, with multiple-testing adjustments

## Interpretation and limitations
This is an exploratory analysis, not a validated predictive model. The sample is small and contains repeated samples from the same drillholes. Correlations do not imply causation; assay values may be affected by detection limits and compositional effects. The spatial join links flotation samples to nearby point assays, not necessarily to their exact source intervals. The definition of `xr` remains a working assumption until checked against the source paper.

## Reproducibility note
The notebook's outputs are cleared in the portfolio copy to avoid showing stale results from code that has since changed. Run all cells with the input data available to regenerate tables and figures.
