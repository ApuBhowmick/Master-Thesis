# **Two-Step Deep Learning for Central Venous Catheter Tip Classification in Chest X-rays**
## Overview
This repository contains the code, data, and visual outputs for my Master's thesis in Statistics and Data Science at Hasselt University (Academic Year 2025-2026).

The project proposes an automated two-step classification system that identifies whether a Central Venous Catheter (CVC) tip is correctly positioned or malpositioned within the right atrium. By extending a full-mask EfficientNet-B7 baseline, this research introduces a novel thickness-based tip detection algorithm and a tip-dot EfficientNet-B7 model, achieving a highly discriminative two-step classification pipeline.

## Repository Structure
The repository is organized into the following directories and files based on the pipeline's workflow:

* **`Code File/`**: Contains the core Jupyter notebooks for the project.
  * `catheter_tip_efficientnetB7_only_tip_position.ipynb`: Implements the tip detection algorithm, feature engineering, classical ML evaluation, and the training of the tip-dot EfficientNet-B7 model.
  * `Efficient NetB7_Weights.ipynb`: Contains the baseline full-mask model training, the two-step routing classifier, and comprehensive sensitivity/specificity analysis.
* **`predicted_masks/`**: The input binary segmentation masks of the catheter tube and right atrium generated via a UNet++ pipeline. 
* **`debug_visuals/`**: Pipeline overlays and visual diagnostics generated during the centreline and tip extraction process. Includes the side-by-side Gaussian tip-dot overlays.
* **`Image output/`**: Evaluation plots, including ROC curves, standard logistic regression coefficient plots, and cross-validated confusion matrices.
* **`catheter_tip_features_ml_ready.csv`**: The extracted and normalized spatial features (e.g., `tip_depth_in_atrium_norm`, `mean_tip_radius`) used to train the classical machine learning classifiers (Logistic Regression, Random Forest, XGBoost).
* **`atriumandcatheter.xlsx`**: The ground-truth clinical labels (correctly placed vs. malpositioned) and metadata provided by the radiologists.

## Methodology
The classification pipeline operates in three main steps:
1. **Tip Detection & Feature Extraction:** The catheter mask is skeletonised, and the clinical tip is located using a strict thickness-based rule. Six numerical features are derived from this coordinate.
2. **Tip-Dot Model:** For reliably detected tips, an EfficientNet-B7 model is trained using a Gaussian dot representation of the tip overlaid on the atrium mask.
3. **Two-Step Routing:** Images with reliable tip detections (200 images) are evaluated by the tip-dot model, while ambiguous skeletons (20 images) are routed to a full-mask EfficientNet-B7 model.

## Key Results
* **Classical ML:** A Logistic Regression model using just two hand-crafted features confirmed that tip location alone holds strong discriminative power, achieving an AUC of up to 0.900.
* **Two-Step Classifier:** The ensemble system achieved an out-of-fold AUC of 0.965 and an accuracy of 0.914.
* **Clinical Safety:** The routing strategy produced a sensitivity of 0.931 and a specificity of 0.899, improving specificity by +0.067 over the previous full-mask baseline (successfully identifying 9 out of 10 malpositioned catheters).

## Software & Dependencies
The codebase was developed in Python 3.13 and executed on the Vlaams Supercomputer Centrum (VSC, Leuven). 
* **Deep Learning:** `PyTorch 2.12`, `timm 1.0.27`
* **Machine Learning:** `scikit-learn 1.9`
* **Computer Vision & Image Processing:** `scikit-image 0.26`, `OpenCV 4.13`, `albumentations 2.0`
* **Data Manipulation:** `NumPy 1.26`, `pandas 3.0`

## Acknowledgements
* **Author:** Apu Chandra Bhowmick
* **Internal Supervisor:** Prof. dr. Tomasz Burzykowski
* **Co-supervisor:** Prof. Dirk Valkenborg
* **External Supervisor:** Tomasz Hryszko
* **Institution:** Hasselt University, School for Information Technology
