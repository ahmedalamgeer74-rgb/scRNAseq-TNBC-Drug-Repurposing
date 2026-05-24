# Raw Transcriptomic Data Placeholder

The single-cell RNA-seq expression matrix used in this project (from the Wu et al. 2021 breast cancer atlas) is too large to be hosted directly on GitHub due to platform file-size limitations.

### How to replicate this dataset locally:
1. Download the raw sparse matrices and cell metadata from the Gene Expression Omnibus (GEO) using accession number **GSE176078**.
2. Place the downloaded expression files directly inside this `data/` directory on your local machine.
3. Run the processing notebooks inside the `notebooks/` directory to automatically parse the data.