# Automated Classification of Central Venous Catheter Tip Position in Chest Radiographs
**A Two-Step Deep Learning Approach with Tip-Point Feature Engineering**[cite: 7]

## Overview
This repository contains the code, data, and visual outputs for my Master's thesis in Statistics and Data Science at Hasselt University (Academic Year 2025-2026)[cite: 7].

The project proposes an automated two-step classification system that identifies whether a Central Venous Catheter (CVC) tip is correctly positioned or malpositioned within the right atrium[cite: 7]. By extending a full-mask EfficientNet-B7 baseline, this research introduces a novel thickness-based tip detection algorithm and a tip-dot EfficientNet-B7 model, achieving a highly discriminative two-step classification pipeline[cite: 7].

## Repository Structure
The repository is organized into the following directories and files based on the pipeline's workflow:

* **`Code File/`**: Contains the core Jupyter notebooks for the project[cite: 7].
  * `catheter_tip_efficientnetB7_only_tip_position.ipynb`: Implements the tip detection algorithm, feature engineering, classical ML evaluation, and the training of the tip-dot EfficientNet-B7 model[cite: 7].
  * `Efficient NetB7_Weights.ipynb`: Contains the baseline full-mask model training, the two-step routing classifier, and comprehensive sensitivity/specificity analysis[cite: 7].
* **`predicted_masks/`**: The input binary segmentation masks of the catheter tube and right atrium generated via a UNet++ pipeline[cite: 7]. 
* **`debug_visuals/`**: Pipeline overlays and visual diagnostics generated during the centreline and tip extraction process[cite: 7]. Includes the side-by-side Gaussian tip-dot overlays[cite: 7].
* **`Image output/`**: Evaluation plots, including ROC curves, standard logistic regression coefficient plots, and cross-validated confusion matrices[cite: 7].
* **`catheter_tip_features_ml_ready.csv`**: The extracted and normalized spatial features (e.g., `tip_depth_in_atrium_norm`, `mean_tip_radius`) used to train the classical machine learning classifiers (Logistic Regression, Random Forest, XGBoost)[cite: 7].
* **`atriumandcatheter.xlsx`**: The ground-truth clinical labels (correctly placed vs. malpositioned) and metadata provided by the radiologists[cite: 7].

## Methodology
The classification pipeline operates in three main steps[cite: 7]:
1. **Tip Detection & Feature Extraction:** The catheter mask is skeletonised, and the clinical tip is located using a strict thickness-based rule[cite: 7]. Six numerical features are derived from this coordinate[cite: 7].
2. **Tip-Dot Model:** For reliably detected tips, an EfficientNet-B7 model is trained using a Gaussian dot representation of the tip overlaid on the atrium mask[cite: 7].
3. **Two-Step Routing:** Images with reliable tip detections (200 images) are evaluated by the tip-dot model, while ambiguous skeletons (20 images) are routed to a full-mask EfficientNet-B7 model[cite: 7].

## Key Results
* **Classical ML:** A Logistic Regression model using just two hand-crafted features confirmed that tip location alone holds strong discriminative power, achieving an AUC of up to 0.900[cite: 7].
* **Two-Step Classifier:** The ensemble system achieved an out-of-fold AUC of 0.965 and an accuracy of 0.914[cite: 7].
* **Clinical Safety:** The routing strategy produced a sensitivity of 0.931 and a specificity of 0.899, improving specificity by +0.067 over the previous full-mask baseline (successfully identifying 9 out of 10 malpositioned catheters)[cite: 7].

## Software & Dependencies
The codebase was developed in Python 3.13 and executed on the Vlaams Supercomputer Centrum (VSC, Leuven)[cite: 7]. 
* **Deep Learning:** `PyTorch 2.12`, `timm 1.0.27`[cite: 7]
* **Machine Learning:** `scikit-learn 1.9`[cite: 7]
* **Computer Vision & Image Processing:** `scikit-image 0.26`, `OpenCV 4.13`, `albumentations 2.0`[cite: 7]
* **Data Manipulation:** `NumPy 1.26`, `pandas 3.0`[cite: 7]

## Acknowledgements
* **Author:** Apu Chandra Bhowmick[cite: 7]
* **Internal Supervisor:** Prof. dr. Tomasz Burzykowski[cite: 7]
* **Co-supervisor:** Prof. Dirk Valkenborg[cite: 7]
* **External Supervisor:** Tomasz Hryszko
* **Institution:** Hasselt University, School for Information Technology[cite: 7]
