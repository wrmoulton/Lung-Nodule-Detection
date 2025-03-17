
# Lung Nodule Detection using MONAI and Machine Learning

This project utilizes advanced medical imaging techniques, deep learning models, and MONAI (Medical Open Network for AI) to automate the detection of lung nodules from CT scan data. Early detection of lung nodules is crucial in diagnosing various lung conditions, including lung cancer. The workflow includes comprehensive steps such as data preprocessing, image transformation, annotation processing, model training, and evaluation.

## Overview

The key components of the project are:

- **Data Handling:** Preprocessing DICOM medical images and converting them to more usable formats (NIfTI, MHD).
- **Image Transformation:** Applying spatial normalization, orientation, and resampling techniques to standardize input data.
- **Mask Generation:** Using annotations to create accurate lung nodule masks for supervised learning.
- **Model Training & Inference:** Utilizing MONAI’s pipeline and nnDetection's detection models for training and evaluation.
- **Evaluation:** Measuring model performance for accurate lung nodule detection to aid early diagnosis.

## Techniques Used

### 1. Data Preprocessing
- **DICOM to MHD/NIfTI Conversion:**  
  Utilized `SimpleITK` to convert raw DICOM images into `.mhd` and `.nii.gz` formats, facilitating model training and processing.
  
- **Metadata Extraction:**  
  Extracted essential metadata (patient ID, coordinates, nodule size) from CSV files to assist in labeling.

### 2. Image Transformation & Normalization
Applied the following transformations using **MONAI**:

- **Channel Normalization:** `EnsureChannelFirstd` to standardize image channels.
- **Orientation Standardization:** `Orientationd` with 'RAS' axcodes to maintain consistency.
- **Spatial Resampling:** `Spacingd` to unify voxel spacing across datasets.
- **Data Type Conversion:** Ensured float precision types compatible with PyTorch.

### 3. Mask Generation
- **Mask Creation with Annotations:**  
  Leveraged `nnDetection`'s `create_circle_mask_itk()` method to generate 3D spherical masks centered around annotated lung nodules, based on provided nodule diameter and coordinates.

- **Parallel Processing:**  
  Implemented multiprocessing pools to efficiently process large volumes of CT scans and mask generation.

### 4. Dataset Splitting
Implemented custom scripts to divide datasets into training, validation, and testing folds, ensuring balanced distribution using **10-fold cross-validation**.

### 5. Model Training
- **nnDetection Framework:**  
  Adopted nnDetection’s 3D detection models optimized for medical imaging tasks.
  
- **Training Pipeline Configuration:**  
  Configured model parameters and paths through generated JSON environment files, specifying hyperparameters, model checkpoints, and data directories.

### 6. Evaluation & Inference
- Evaluated trained models on unseen CT scans using preprocessed data.
- Inference results (bounding boxes of detected nodules) saved and analyzed.

## Dependencies

Key dependencies used in this project:

- `MONAI`
- `SimpleITK`
- `PyTorch`
- `pydicom`
- `nnDetection`
- `loguru`
- `hydra-core`
- `pandas`
- `omegaconf`

To install:

```bash
pip install monai SimpleITK pydicom loguru hydra-core pandas omegaconf gitpython fire pytorch-ignite
git clone https://github.com/MIC-DKFZ/nnDetection.git
```

## Recommended Alternative (Simplified Process)

A more straightforward approach for lung nodule detection and segmentation can be achieved through:

- **3D Slicer with MONAI Plugin:**  
  Allows for easier data visualization, annotation, and model application.

Refer to this guide for more details:  
[Using MONAI Bundle and Model Zoo to Segment Medical Imaging Data](https://medium.com/@davesimms44/using-monai-bundle-and-the-monai-model-zoo-to-segment-medical-imaging-data-7ade49699248)


## Citation & Credits

- **MONAI:**  
  [https://monai.io](https://monai.io)
  
- **nnDetection:**  
  [https://github.com/MIC-DKFZ/nnDetection](https://github.com/MIC-DKFZ/nnDetection)
