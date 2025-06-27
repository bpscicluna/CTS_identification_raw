# Consensus Transcriptomic Subtype of Sepsis

This R package provides tools to classify new patients into **Consensus Transcriptomic Subtypes (CTS)** of sepsis based on gene expression data. It supports batch correction, classification using a pre-trained random forest model, and visualization via heatmaps and silhouette plots.

## 📦 Installation

You can install the development version from GitHub using:

```r
# install.packages("devtools")
devtools::install_github("bpscicluna/ConsensusTranscriptomicSubtype")
```

## 🚀 Quick Start

```r
library(ConsensusTranscriptomicSubtype)

# Load your new expression data
# Must be a data.frame or matrix with Ensembl gene IDs as rownames
# If it's a data.frame, it must have a "gene" column
new_data <- read.csv("your_data.csv")

# Run classification
result <- run_subtype_classifier(new_expr_data = new_data)

# View predictions
head(result$predictions)

# Visualize silhouette plot
plot(result$silhouette)
```

## 🧬 Input Requirements

- `new_expr_data`: Gene expression matrix with **Ensembl gene IDs** as row names.
  - If it's a `data.frame`, a column named `"gene"` is required and will be used as row names.
- Default reference data (`exp_core_g`, `core_samples`) is included in the package.

## 📊 Outputs

- `predictions`: Data frame of sample IDs and predicted CTS labels (1, 2, or 3)
- `expression_corrected`: Batch-corrected expression matrices
- `silhouette`: Silhouette object for subtype separation quality
- `rf_model`: Random forest classifier object

## 📁 Optional PDF Output

Save visualizations by specifying file paths:

```r
run_subtype_classifier(
  new_expr_data = new_data,
  heatmap_file = "CTS_Heatmap.pdf",
  silhouette_file = "CTS_Silhouette.pdf"
)
```

## 🧠 Citation

If you use this package, please cite the corresponding publication describing the CTS of sepsis (citation coming soon).

## 🔧 License

MIT License © Brendon P. Scicluna
