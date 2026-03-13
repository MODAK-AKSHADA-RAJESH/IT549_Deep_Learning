# Dataset Description

This project uses an image dataset designed for **Air Quality Index (AQI) classification**.  
The dataset contains outdoor images along with labels indicating the corresponding AQI category.

The goal of the dataset is to allow machine learning models to learn visual patterns associated with different air quality conditions.

---

# Dataset Structure

The dataset is organized into two main components:

```
dataset/
│
├── data.csv
└── sampled_images/
    ├── image_001.jpg
    ├── image_002.jpg
    ├── image_003.jpg
    └── ...
```

### 1. data.csv

This file contains metadata for each image in the dataset.

Each row corresponds to one image and includes the following fields:

| Column | Description |
|------|------|
| **Filename** | Name of the image file stored in `sampled_images/` |
| **AQI_Class** | The AQI category label assigned to the image |

Example:

| Filename | AQI_Class |
|------|------|
| img_001.jpg | Good |
| img_002.jpg | Moderate |
| img_003.jpg | Unhealthy |

---

### 2. sampled_images/

This directory contains the actual images referenced in `data.csv`.  
Each image represents an outdoor scene captured under different atmospheric conditions.

The filenames listed in `data.csv` correspond directly to the images stored in this folder.

---

# Data Preprocessing

Before training the models, the following preprocessing steps were applied:

1. **Image Resizing**

All images were resized to:

```
224 × 224 pixels
```

This size is commonly used for CNN architectures and pretrained models such as ResNet.

2. **Normalization**

Pixel values were normalized to improve training stability and convergence.

3. **Label Encoding**

The AQI class labels were converted into numerical values so they could be used by the neural network during training.

---

# Dataset Splitting

To evaluate model performance effectively, the dataset was divided into three subsets:

| Split | Percentage | Purpose |
|------|------|------|
| Training Set | 70% | Used to train the model |
| Validation Set | 15% | Used to tune model parameters |
| Test Set | 15% | Used for final performance evaluation |

---

# Intended Use

This dataset is used for **image classification tasks related to air quality prediction**.  
It allows models to learn correlations between visual environmental cues (such as haze, visibility, and lighting) and AQI categories.

The dataset is intended primarily for **educational and experimental purposes** in deep learning and computer vision.

---

# Notes

- The dataset is relatively small compared to large-scale vision datasets.
- Performance of deep learning models may vary depending on architecture, training strategy, and preprocessing techniques.
- Transfer learning methods can sometimes improve results when working with limited datasets.
  
