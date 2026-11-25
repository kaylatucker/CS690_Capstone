# DASC 690 Capstone — Olist

## Seller Performance & Customer Experience Analysis in E-Commerce

This project uses business data analysis and statistical methods to examine seller performance and customer satisfaction in the Olist Brazilian e-commerce marketplace.

**Research question:** Which operational, product, and geographic factors are most strongly associated with seller performance and customer satisfaction?

**Dataset:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (2016–2018).

## Requirements and setup

- Python 3.14.7
- VS Code with the Python and Jupyter extensions
- Python libraries listed in `requirements.txt`

Clone the repository and install the dependencies as necessary:

```bash
git clone https://github.com/kaylatucker/CS690_Capstone.git
cd CS690_Capstone
python -m pip install -r requirements.txt
```
## Reproducing the analysis

1. Open the repository root in VS Code and select the Python environment containing the installed dependencies as the notebook kernel.
2. Ensure the nine source CSV files are in `02_data/raw/`. Notebooks 01–03 also retrieve the dataset through KaggleHub.
3. Run all notebooks in `03_notebooks/` in numerical order (01–12), restarting the kernel before running each notebook.
4. Notebooks 03–05 regenerate the processed datasets. Notebook 11 validates the analysis, and Notebook 12 exports the final figures.

## Folder guide
- `00_admin/` — timeline, progress log, decision log
- `01_research/` — for references and research
- `02_data/raw/` — untouched source data
- `02_data/processed/` — clean or manipulated data
- `03_notebooks/` — exploratory and statistical analysis notebooks
- `04_outputs/figures/` — final/exported charts
- `04_outputs/tables/` — final/exported tables
- `05_reports/` — report drafts and supporting documents
- `06_presentations/` — presentation materials
