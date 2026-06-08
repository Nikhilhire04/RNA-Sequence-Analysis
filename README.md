# Breast Cancer RNA-seq Differential Expression Analysis

RNA-seq analysis pipeline built on TCGA-BRCA data to identify differentially 
expressed genes and enriched biological pathways in breast cancer tumor vs 
normal tissue.

---

## Background

Breast cancer is one of the most heterogeneous cancers, with complex transcriptional 
changes driving tumor progression. This project uses publicly available TCGA-BRCA 
RNA-seq data to characterize gene expression differences between primary tumor and 
normal adjacent tissue samples using a reproducible Python-based pipeline.

---

## Dataset

- **Source:** TCGA-BRCA via GDC Data Portal
- **Samples:** 145 total — 99 Primary Tumor, 46 Solid Tissue Normal
- **Workflow:** STAR - Counts (HTSeq augmented)
- **Genes:** 26,575 after low-count filtering

---

## Pipeline
| Stage | Description | Tools |
|-------|-------------|-------|
| 1 | Data acquisition | GDC API, requests |
| 2 | QC & filtering | pandas, matplotlib |
| 3 | Normalization | pydeseq2 (VST) |
| 4 | Exploratory analysis | PCA, heatmap, correlation | 
| 5 | Differential expression | pydeseq2, volcano plot |
| 6 | Pathway enrichment | gseapy, GSEA, GO, KEGG |

---

## Key Results

### Differential Expression
- **Total DEGs:** 4,092 (|log2FC| > 1.5, padj < 0.05)
- **Upregulated in tumor:** 2,319 genes
- **Downregulated in tumor:** 1,773 genes

### GSEA — Hallmark Pathways (top hits)
| Pathway | NES | FDR |
|---------|-----|-----|
| G2-M Checkpoint | 2.68 | 0.01 |
| E2F Targets | 2.66 | 0.01 |
| Myc Targets V1 | 2.19 | 0.01 |
| Adipogenesis | -2.48 | 0.01 |

### GO Biological Process (top hits)
- Extracellular Matrix Organization
- Mitotic Spindle Assembly Checkpoint Signaling
- Cytokine-cytokine receptor interaction

---

## Figures

| PCA | Volcano Plot |
|-----|-------------|
| ![PCA](figures/pca_plot.png) | ![Volcano](figures/volcano_plot.png) |

| Heatmap | Enrichment |
|---------|------------|
| ![Heatmap](figures/heatmap.png) | ![Enrichment](figures/enrichment_dotplot.png) |

---

## Interpretation

The upregulation of G2-M checkpoint and E2F target genes points to 
uncontrolled cell cycle progression in tumor samples — a well established 
hallmark of breast cancer. Extracellular matrix remodeling pathways showing 
strong enrichment is consistent with tumor invasion biology. Downregulation 
of adipogenesis-related genes reflects the loss of normal breast adipose tissue 
identity in tumor samples, which has been reported in several BRCA studies.

---

## Project Structure
breast-cancer-rnaseq/
├── notebooks/
│   ├── 01_data_acquisition.ipynb
│   ├── 02_qc_filtering.ipynb
│   ├── 03_normalization.ipynb
│   ├── 04_eda.ipynb
│   ├── 05_differential_expression.ipynb
│   └── 06_pathway_enrichment.ipynb
├── results/
│   ├── DEGs_with_symbols.csv
│   ├── gsea_results.csv
│   └── ora_results.csv
├── figures/
│   ├── pca_plot.png
│   ├── volcano_plot.png
│   ├── heatmap.png
│   └── enrichment_dotplot.png
├── requirements.txt
└── README.md
---

## Requirements
pandas
numpy
requests
matplotlib
seaborn
scikit-learn
pydeseq2
gseapy
mygene
---

## How to Run

```bash
git clone https://github.com/Nikhilhire04/RNA-Sequence-Analysis
cd breast-cancer-rnaseq
pip install -r requirements.txt
# open notebooks in order 01 → 06
```

---

## References

- TCGA-BRCA dataset via GDC portal
- Love et al. (2014) — DESeq2
- Subramanian et al. (2005) — GSEA
- MSigDB Hallmark gene sets
