# Cancer-Subtype-Classification-by-ML 🧬🔬
Machine learning–based cancer subtype classification using RNA-seq expression data from the UCI TCGA Pan-Cancer (HiSeq) dataset, with PCA-driven dimensionality reduction.
![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

## 🌟 Project Overview
This project addresses a critical challenge in oncology: **identifying the tissue of origin for metastatic cancers.** While many cancers look similar under a microscope, their genetic "instructions" (transcriptome) remain unique to the organ where they started. 

Using **The Cancer Genome Atlas (TCGA)** Pan-Cancer dataset, I developed a machine learning pipeline that classifies five major cancer types with **100% accuracy**. This demonstrates that machine learning can decode the molecular "fingerprints" of tumors to assist in precise clinical diagnostics.


## 📊 Key Results
- **Model Accuracy:** 100% (Precision, Recall, and F1-Score of 1.00 for all classes).
- **Dimensionality Reduction:** Condensed 20,531 gene features into the top 50 Principal Components (PCs), capturing **63.03%** of the total biological variance.
- **Subtypes Classified:**
  * **BRCA:** Breast Invasive Carcinoma
  * **KIRC:** Kidney Renal Clear Cell Carcinoma
  * **LUAD:** Lung Adenocarcinoma
  * **PRAD:** Prostate Adenocarcinoma
  * **COAD:** Colon Adenocarcinoma

### 1. The Transcriptomic Landscape (PCA)

The PCA plot reveals that different cancer types form distinct "islands." Even with 20,000 genes reduced to just 2 dimensions, the clusters do not overlap, proving that each organ has a fundamentally different genetic dialect.

### 2. Confusion Matrix

The confusion matrix shows a perfect diagonal line, meaning every single sample in the test set was correctly identified.


## 🧠 Biological Interpretation (For Non-Experts)
1. **The "Genetic Dialect":** Every organ in our body uses the same DNA library but reads different chapters. Our model "listens" to this dialect to determine if a tumor started in the lung or the kidney.
2. **Precision Medicine:** By identifying the specific genes used for classification, we move from "one-size-fits-all" treatment to **targeted therapy** based on a patient’s unique molecular profile.
3. **Solving "Unknown Primaries":** When cancer spreads, doctors sometimes can't find the source. This model provides a "molecular GPS" to trace a tumor back to its home organ.


## 🛠️ Technical Workflow
The pipeline is designed to solve the **"Curse of Dimensionality"** ($p \gg n$), where we have 20,000+ genes but only 801 patients.

1.  **Preprocessing:** Applied $log_2(x+1)$ transformation to stabilize the high variance inherent in RNA-Seq count data.
2.  **Feature Scaling:** Z-score normalization to ensure every gene contributes equally to the initial model.
3.  **Dimensionality Reduction (PCA):** Filtered out 99% of genetic noise, keeping only the 50 most informative Principal Components.
4.  **Classification (SVM):** A Linear Support Vector Machine was used to find the optimal boundary between different tissue types.
5.  **Feature Importance:** Mapped SVM weights back to the original gene space to identify the top **Biomarkers** driving the decisions.


## 🧬 Diagnostic Biomarkers (Top 10 Genes)
The model identified specific genes as the primary drivers for classification. In this UCI dataset, genes are labeled by index (e.g., `gene_5237`).

| Rank | Feature | Importance Score | Clinical Context |
| :--- | :--- | :--- | :--- |
| 1 | gene_5237 | 0.000746 | Primary tissue-specific driver |
| 2 | gene_4035 | 0.000713 | Differentiates solid tumor types |
| 3 | gene_4397 | 0.000710 | Key metabolic marker |
| ... | ... | ... | ... |

*Note: In this UCI version, placeholders are used for gene names to maintain data uniformity, but the biological signal remains intact.*

### Understanding Gene Identifiers
In the **UCI Gene Expression Cancer RNA-Seq** dataset, original gene symbols (like *BRCA1*) were replaced with placeholder labels (`gene_XX`) for data uniformity.

**How to map these to real gene symbols:**
- **Order Preservation:** The feature order (0 to 20,530) is preserved from the original **TCGA PANCAN** submission.
- **Cross-Reference:** Researchers map these indices back using the original probe names from the [Synapse TCGA Repository (syn4301332)](https://www.synapse.org/#!Synapse:syn4301332).
- **Clinical Relevance:** High-ranking genes often correspond to known biomarkers, such as *KLK3* for Prostate cancer.


## 📁 Repository Structure
- `Cancer_Subtype_ML_Pipeline.ipynb`: The complete Python pipeline ready for Google Colab.
- `plots/`: High-resolution PNGs of the results.
- `LICENSE`: MIT License.

## How to Reproduce
1. Open the `.ipynb` file in Google Colab.
2. Use the provided `!wget` command to download the TCGA-PANCAN dataset.
3. Run all cells to generate the plots and classification report.

## Acknowledgments & Citations
- **Data Source:** UCI Machine Learning Repository [Dataset ID: 401].
- **TCGA Network:** The results shown here are based upon data generated by the TCGA Research Network: [https://www.cancer.gov/tcga](https://www.cancer.gov/tcga).
- **UCI Citation:** Kelly, M., Longjohn, R., & Nottingham, K. (2024). The UCI Machine Learning Repository.


##  License
This project is licensed under the **MIT License**—free to use for research and educational purposes.
