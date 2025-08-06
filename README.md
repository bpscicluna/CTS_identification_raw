# Consensus Transcriptomic Subtypes of Sepsis - R Analysis

**Author:** Scicluna  
**Last Updated:** August 2025

## Overview

This repository contains the R script used to perform the computational analysis for the identification, validation, and clinical characterization of three **Consensus Transcriptomic Subtypes (CTSs)** in sepsis.

The analysis integrates leukocyte transcriptomics data from two major discovery cohorts, **MARS** and **GAinS**, to build a robust classification model. This model is subsequently used to classify patients in an independent clinical trial cohort, **VANISH**, to explore the interaction between subtype and corticosteroid treatment efficacy. The script also performs comprehensive analyses linking the CTSs to key clinical outcomes such as mortality, organ failure (SOFA score), and infection source.

## Key Features of the Analysis

  * **Derivation of Consensus Subtypes:** Utilizes existing subtype assignments and Markov Clustering (MCL) on Jaccard distances to define a stable set of core patient samples for each subtype.
  * **Machine Learning Classifier:** Develops a Random Forest classifier based on the transcriptomes of core samples to assign any new patient sample to a CTS.
  * **Performance Evaluation:** Assesses classifier accuracy using Out-Of-Bag (OOB) error estimates, confusion matrices, and silhouette plots.
  * **Biological Visualization:** Generates heatmaps of the key classifier genes that define the biological signature of each subtype.
  * **External Validation & Clinical Interaction:** Applies the classifier to the VANISH trial cohort and uses a logistic regression model (`glm`) to test for a significant interaction between CTS, hydrocortisone treatment, and 28-day mortality.
  * **Clinical Association Analysis:** Associates the CTSs with clinical variables in the MARS and GAinS cohorts, including mortality, SOFA scores, pneumonia, and abdominal sepsis, using appropriate statistical tests (`dunn.test`, `chisq.test`).

## Code Structure

The R script is organized into several logical sections:

1.  **Library Loading:** Loads all required R packages for the analysis.
2.  **Initial Subtype Overlap:** Generates a binary heatmap to visualize the concordance between previously published sepsis subtype models (e.g., SRS, Stanford) in the MARS cohort.
3.  **MCL Clustering:** Performs Markov Clustering with varying inflation parameters to identify robust clusters from a Jaccard distance matrix.
4.  **Random Forest Classifier Construction:**
      * Builds a Random Forest model using a defined set of "core" patient samples.
      * Prints the model's performance metrics (OOB error, confusion matrix).
      * Calculates and plots silhouette widths to assess cluster cohesion and separation.
5.  **Classifier Gene Heatmap:** Visualizes the expression of the top classifier genes across all samples, annotated by their assigned CTS.
6.  **Application to the VANISH Cohort & Corticosteroid Interaction:**
      * Applies the trained Random Forest model to classify patients from the VANISH trial.
      * Performs statistical analysis (`glm`, `allEffects`) to model and visualize the interaction between CTS, drug assignment (hydrocortisone vs. placebo), and 28-day mortality. Generates probability plots using `ggplot2`.
7.  **Clinical Associations in MARS & GAinS:**
      * Merges CTS assignments with clinical data from the discovery cohorts.
      * Performs statistical tests and generates plots (violin plots for SOFA, bar plots for categorical outcomes) to assess the relationship between CTS and clinical phenotypes.
8.  **Corticosteroid Use in MARS:** Investigates the baseline association between CTS and corticosteroid administration in the MARS observational cohort.
9.  **Further Analyses (Mentioned):** The script notes that downstream analyses such as Gene Set Enrichment Analysis (GSEA) and single-cell data analysis (AUCell) were performed separately.

## Dependencies

### R Libraries

To run this script, you will need the following R packages:

```r
library(mixOmics)
library(limma)
library(sva)
library(pheatmap)
library(RColorBrewer)
library(MCL)
library(jaccard)
library(cluster)
library(ggplot2)
library(effects)
library(rcompanion)
library(twang)
# Note: randomForest library is used but not explicitly loaded at the top.
```

### Data Files

This script requires several input data files (`.csv`, `.txt`) which are **not included** in this repository due to patient data privacy and collaborator agreements. The necessary files include, but are not limited to:

  * Normalized gene expression matrices for the MARS, GAinS, and VANISH cohorts.
  * Files containing subtype assignments and clinical data annotations.
  * Pre-calculated distance matrices.

## Usage

To reproduce this analysis, you would need access to the required data files. The script should be run section by section, ensuring that the input file paths are correctly specified for your local environment. Due to the absence of the data, this script serves primarily as a methodological reference for the published work.
