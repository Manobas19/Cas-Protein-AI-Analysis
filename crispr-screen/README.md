# High-throughput CRISPR screen: three-month project

A Google Colab / Jupyter notebook for analysing pooled CRISPR knockout or CRISPRi sgRNA counts, with a 12-week research plan.

[Open in Google Colab](https://colab.research.google.com/github/Manobas19/Cas-Protein-AI-Analysis/blob/main/crispr-screen/High_Throughput_CRISPR_Screen_3_Month_Project.ipynb)

## AI, machine learning and analysis packages

The implemented machine-learning method is **principal component analysis (PCA)** using scikit-learn. PCA is an unsupervised dimensionality-reduction method used here to explore sample patterns and quality. The notebook does not train a supervised prediction model, neural network or generative AI model.

| Package / tool | Use in this notebook |
|---|---|
| **scikit-learn** (`sklearn`) | PCA for sample exploration and QC; the ML package actually used |
| **NumPy** (`numpy`) | Arrays, simulated counts, numerical calculations and random number generation |
| **pandas** (`pandas`) | Count tables, metadata, filtering, grouping and CSV/TSV input/output |
| **SciPy** (`scipy`) | Exploratory paired/Welch t-tests and hypergeometric pathway tests |
| **Matplotlib** (`matplotlib`) | Figures and image export |
| **seaborn** (`seaborn`) | Statistical visualisation and plot styling |
| **IPython** (`IPython`) | Notebook table display |
| **Google Colab** (`google.colab`) | Upload/download dialogs in Colab; supplied by the Colab environment |
| **MAGeCK** | Optional external, count-aware CRISPR gene analysis; requires separate installation or Galaxy execution |

NumPy, pandas, SciPy and the plotting libraries support the analysis; they are not independently trained AI models. TensorFlow, PyTorch, XGBoost, LightGBM, transformers and LLM APIs are not used or required by this notebook.

Python standard-library modules used: `importlib.util`, `importlib.metadata`, `subprocess`, `sys`, `pathlib`, `json`, `hashlib`, `platform`, `shutil`, `warnings` and `shlex`. They need no separate pip installation.

## Run the project

1. Open the notebook using the Colab link above.
2. Select **Runtime → Run all**. A CPU runtime is sufficient.
3. Leave `USE_DEMO=True` for the reproducible simulated example.
4. For real data, set `USE_DEMO=False`, specify your trait and species, and supply the input files described below.
5. Download the results ZIP before closing the Colab session.

For local Jupyter, install the dependencies with `python -m pip install -r requirements.txt`, then open the notebook in your Jupyter environment. The real-data upload dialogs use Colab; adapt those cells to local file paths if working in Jupyter.

Dependencies are unpinned because the uploaded notebook installs only missing packages. Each run exports its actual package versions to `environment_versions.json`; retain that record for reproduction.

## Required real-data inputs

- `counts.csv` or `counts.tsv`: raw nonnegative integer counts, with columns `sgRNA`, `Gene`, and one column per sample.
- `metadata.csv` or `metadata.tsv`: `sample`, `group` (control/treatment), `replicate`, and optional `batch` / `pair`.
- Optional `control_guides.csv`: validated neutral guide IDs in a column named `sgRNA`.
- Optional local `.gmt` file: gene sets matching the species and identifier system for pathway analysis.

The exploratory analysis requires at least three independent biological samples per condition. Aggregate technical replicates first. The simple baseline rejects multiple batches; use an appropriate covariate-aware model for such designs.

## Workflow and outputs

Input/design validation → count QC → filtering and normalization → sample PCA → guide effects → exploratory gene statistics with BH adjustment → candidate visualisation → optional MAGeCK execution/import → optional pathway enrichment → evidence table and results ZIP.

Outputs include guide effects, all tested genes, exploratory candidates, figures, MAGeCK-ready raw counts, metadata, configuration, environment versions, input hashes and an analysis summary.

## Three-month plan

| Weeks | Main work |
|---|---|
| 1–2 | Research question, study design and data provenance |
| 3–4 | QC, annotation review and frozen analysis plan |
| 5–6 | Normalization, guide effects and exploratory ranking |
| 7–8 | MAGeCK analysis and sensitivity review |
| 9–10 | Pathway interpretation and literature evidence |
| 11–12 | Validation proposals, figures, final report and repository |

## Interpretation

The default inputs are simulated and do not represent biological discoveries. Exploratory t-tests are not MAGeCK results. MAGeCK is disabled by default and must be run or its results imported separately. Screen hits remain candidates requiring independent validation; enrichment or statistical significance alone does not establish causation. Separate MAGeCK enrichment and depletion FDR columns do not provide a single FDR guarantee for their union.

This workflow analyses pooled sgRNA count screens, rather than RNA-seq expression, microscopy plates or single-cell Perturb-seq.

## Data availability and references

This repository folder contains the uploaded notebook and documentation. It contains no real experimental input data or biological findings. The notebook generates its example counts locally.

- [MAGeCK original paper](https://doi.org/10.1186/s13059-014-0554-4)
- [MAGeCK installation](https://sourceforge.net/p/mageck/wiki/installation/)
- [MAGeCK usage](https://sourceforge.net/p/mageck/wiki/usage/)
- [MAGeCK output definitions](https://sourceforge.net/p/mageck/wiki/output/)
