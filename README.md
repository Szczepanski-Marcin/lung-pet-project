# 🧠 PET Image Classification for Lung Cancer Subtypes

## 📌 Project Overview

This project explores **lung cancer subtype classification using PET scan data**. The goal is to extract meaningful **radiomics-inspired features** from medical images and train a machine learning model to distinguish between cancer types.

The pipeline demonstrates:

- Medical image preprocessing (DICOM handling)  
- Feature extraction (intensity, texture, shape proxies)  
- Machine learning classification  
- Model evaluation using clinically relevant metrics  

---

## 📊 Dataset

- Source: Lung Cancer PET/CT dataset (DICOM format)  
- Classes:
  - Adenocarcinoma  
  - Squamous Cell Carcinoma  
  - Small Cell Carcinoma  
  - Large Cell Carcinoma  

- Total samples: ~18,500 slices  

> ⚠️ **Important limitations**
> - No tumor segmentation masks available  
> - No patient-level identifiers (possible data leakage)  
> - Slice-level classification instead of patient-level analysis  

---

## ⚙️ Methodology

### 🔹 1. Data Loading & Preprocessing

- DICOM images loaded using `pydicom`  
- Pixel intensities normalized to [0, 1]  
- Empty or invalid images removed  

---

### 🔹 2. Feature Extraction

Each image is represented using three groups of features:

#### 🟦 Intensity Features
- Mean intensity  
- Standard deviation  
- Maximum intensity  
- 10th and 90th percentiles  

#### 🟩 Texture Features (GLCM)
- Contrast  
- Homogeneity  
- Energy  

These features capture spatial intensity patterns in the image.

#### 🟨 Shape Proxy
- Approximate “high-intensity region volume” using percentile thresholding  

> ⚠️ This is a **proxy feature**, not true tumor segmentation.

---

### 🔹 3. Model Training

- Model: **Random Forest Classifier**
- Parameters:
  - `n_estimators = 200`
  - `class_weight = "balanced"`

- Validation strategy:
  - Train/test split (80/20)
  - 5-fold stratified cross-validation  

---

## 📈 Results

### 🔹 Cross-Validation Performance
