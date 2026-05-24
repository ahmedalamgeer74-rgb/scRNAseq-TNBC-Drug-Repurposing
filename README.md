# In Silico Drug Repurposing Pipeline for Triple-Negative Breast Cancer (TNBC) via Single-Cell Transcriptomics and Molecular Docking

An end-to-end bioinformatics and structural biology pipeline that leverages large-scale single-cell RNA sequencing (scRNA-seq) data to identify and structurally validate therapeutic candidates for aggressive breast cancer subpopulations.

---

## Project Overview
Triple-Negative Breast Cancer (TNBC) remains one of the most clinical challenging subtypes of breast cancer due to its highly heterogeneous nature and lack of targeted receptor therapies. This project presents a computational framework that:
1. Stratifies malignant cancer epithelial cell cohorts from clinical trial datasets.
2. Extracts core upregulated pharmacogenetic vulnerability signatures.
3. Screens small molecule databases to uncover signature-reversal drug candidates.
4. Validates structural binding affinity using quantum mechanics/physics-based molecular docking simulations.

---

## Workflow Architecture

### Phase 1: Single-Cell Transcriptomics & Target Discovery
* **Dataset:** Single-cell RNA-seq atlas from Wu et al. (2021) consisting of raw sparse expression matrices and clinical metadata.
* **Processing:** Built a Python-driven data processing pipeline using `Scanpy` to isolate a clean cohort of **24,489 malignant Cancer Epithelial cells**.
* **Stratification:** Segregated the tumor population into ER+ ($n=11,878$), TNBC ($n=10,836$), and HER2+ ($n=1,775$) cells.
* **Signature Extraction:** Performed high-throughput differential gene expression analysis (Wilcoxon rank-sum test) to isolate the top upregulated genomic features unique to the highly aggressive TNBC subgroup.

### Phase 2: Transcriptomic Signature Reversal Screening
* The unique genetic signature was passed to the **L1000CDS2 (LINCS L1000 Characteristic Direction Signature Search Engine)** platform.
* Screened for small-molecule perturbations computationally mapped to completely reverse the expression profile of the driving oncogenic network.
* **Niclosamide** emerged as a top prioritized FDA-approved therapeutic candidate known to target downstream oncogenic signaling networks.

### Phase 3: Structure-Based Molecular Docking Verification
To validate the transcriptomic candidate at the structural biology level, a virtual screening simulation was performed against the human **STAT3 transcription factor** (PDB: `1BG1`), which drives dimerization and nuclear survival signalling in TNBC.

* **Tool Suite:** Schrödinger Suite (Maestro 12.5 / Glide Engine)
* **Protein Preparation:** Preprocessed with the Protein Preparation Wizard; assigned bond orders, added missing hydrogens, optimized H-bond networks, and executed a restrained minimization using the OPLS3e force field.
* **Ligand Preparation:** Niclosamide was optimized via `LigPrep` using Epik at a biological target pH of $7.0 \pm 2.0$.
* **Grid Generation:** A 3D receptor grid box was constructed directly over the SH2 dimerization domain, centered around critical interactive pocket residues **Arg609**, **Ser611**, and **Tyr705**.
* **Simulation Precision:** Glide Standard Precision (SP) flexible docking.

---

## Key Findings & Structural Results

### Docking Affinities
* **Glide Gscore:** `-3.286 kcal/mol`
* **Docking Score:** `-3.219 kcal/mol`
* **Glide Energy:** `-30.268 kcal/mol`

Given that STAT3 is a flat, highly charged protein-protein interaction (PPI) surface without a deep catalytic pocket, the calculated score indicates a stable, structurally favorable binding layout within the shallow SH2 pocket interface.

### Atomic Interaction Map Analysis
A 2D ligand interaction analysis confirmed specific structural configurations that lock the drug candidate within the target pocket:
* **Hydrogen Bonding:** A directional, stable H-bond forms between **ASN 646** and the electronegative oxygen atom of Niclosamide's nitro ($\text{NO}_2$) group.
* **Electrostatic Stabilization:** Strong electronic bridging occurs between the basic guanidinium head of **ARG 688** and the phenolate oxygen of the drug.
* **Hydrophobic Shielding:** The chlorinated benzene ring sits comfortably inside a non-polar pocket formed by **PHE 650, TYR 575, ILE 576, LEU 577,** and **LEU 579**, maximizing van der Waals structural contact.

---

## Software, Tools, & Dependencies
* **Data Science / Transcriptomics:** Python 3.x, `Scanpy`, `Anndata`, `Pandas`, `NumPy`
* **Web Services:** L1000CDS2 Search Engine, PubChem Database, RCSB Protein Data Bank
* **Structural Biology Suite:** Schrödinger Suite (Maestro 12.5, LigPrep, Glide Grid Gen, Glide Ligand Docking)

---

## Acknowledgments
Special thanks to the academic mentors, research directors, and laboratory colleagues who provided access to institutional tools and software ecosystems that made this project possible.