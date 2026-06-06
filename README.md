# 🧬 Cancer Subtype Classification from Gene Expression Profiles

Benchmarking three deep learning architectures — MLP, 1D CNN, and Transformer — 
on TCGA pan-cancer gene expression data for multi-class cancer subtype classification.

## 📊 Results

| Model       | Test Accuracy | F1 Score | Parameters | Training Time |
|-------------|--------------|----------|------------|---------------|
| MLP         | 90.06%       | 85.62%   | 10,578,693 | 62.7s         |
| **1D CNN**  | **99.38%**   | **99.38%**| 2,631,141 | 135.4s        |
| Transformer | 96.89%       | 96.87%   | 129,093    | 841.9s        |

**Key finding:** 1D CNN outperforms both MLP and Transformer in accuracy and F1 
while using 4x fewer parameters than MLP and training 6x faster than Transformer.

## 🗂️ Dataset

- **Source:** TCGA Pan-Cancer gene expression profiles (Kaggle)
- **Samples:** 801 patients, 20,531 gene features
- **Classes:** BRCA, COAD, KIRC, LUAD, PRAD
- **Split:** 80% train / 20% test (stratified)

## 🏗️ Architectures

**MLP** — 3-layer fully connected network (10.6M params)  
Baseline model. Global feature aggregation only, no spatial awareness.

**1D CNN** — 3 convolutional blocks + max pooling + FC head (2.6M params)  
Captures local patterns across the gene expression sequence. Best performer.

**Transformer** — Patch-based 1D Transformer with positional encoding (129K params)  
Most parameter-efficient. Competitive accuracy but significantly slower to train.

## 💡 Key Insights

- Local pattern detection (CNN) outperforms global attention (Transformer) 
  on tabular genomic data — consistent with prior bioinformatics literature.
- MLP's instability during training suggests raw gene expression features 
  benefit from spatial inductive bias.
- Transformer achieves competitive results with 80x fewer parameters than MLP, 
  suggesting strong potential with larger datasets.

## 🚀 Reproducing

```bash
pip install torch scikit-learn pandas numpy matplotlib seaborn
```

1. Download dataset from Kaggle: `tcga-pan-cancer`
2. Run `cancer_classification.ipynb`
## 🔬 Future Work

- Explainability: SHAP values to identify which genes drive classification
- Add copy number variation (CNV) as second modality
- Cross-validation for more robust evaluation
