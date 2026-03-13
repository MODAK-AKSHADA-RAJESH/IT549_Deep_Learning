# Image-Based AQI Classification using CNN and Transfer Learning

**Course:** IT549 – Deep Learning  
**Lab Assignment:** Lab 3 – Image-Based AQI Classification  

**Name:** Akshada Modak  
**Student ID:** 202301485

---

# Project Description

The objective of this project is to build a deep learning model capable of predicting the **Air Quality Index (AQI)** category of a location based on visual information from images. Environmental conditions such as pollution often influence the appearance of outdoor scenes, affecting factors like visibility, color tones, and atmospheric haze. These visual cues can potentially be used by machine learning models to estimate air quality levels.

Two different modeling approaches were explored in this experiment:

- A **Convolutional Neural Network (CNN)** developed and trained from scratch  
- A **pretrained ResNet18 model** applied using **transfer learning**

The purpose of implementing both approaches was to compare how a model trained entirely on the given dataset performs against a model that already contains visual knowledge learned from a large dataset.

---

# Dataset

The dataset used for this experiment contains two main components:

- **data.csv** – a file that stores image filenames and their corresponding AQI class labels  
- **sampled_images/** – a directory containing the image files referenced in the dataset

From the dataset, only the following columns were required:

- **Filename** → used to load the input image  
- **AQI_Class** → the target label representing the air quality category

Before training, all images were resized to **224 × 224 pixels**, which is a commonly used input size for CNN-based architectures. Pixel values were also normalized to ensure stable training behavior.

---

# Methodology

## 1. Data Preparation

The dataset was first loaded using the **pandas** library. Since neural networks require numerical inputs, the AQI class labels were encoded into integer values.

The dataset was then divided into three subsets:

- **Training set:** 70% of the data  
- **Validation set:** 15% of the data  
- **Test set:** 15% of the data  

Image preprocessing was handled using **torchvision.transforms**, which applied resizing, tensor conversion, and normalization before feeding the images into the models.

---

## 2. CNN Model Built from Scratch

The first approach involved designing a **Convolutional Neural Network** using PyTorch.

The architecture consisted of:

- Three **convolutional layers** for extracting spatial features from images  
- **ReLU activation functions** to introduce non-linearity  
- **Max-pooling layers** to reduce spatial resolution and highlight dominant features  
- A **fully connected classifier** for predicting AQI categories

The model was trained using:

- **Adam optimizer** for parameter updates  
- **CrossEntropyLoss** as the loss function for multi-class classification

This model learned visual features directly from the dataset without relying on any pretrained knowledge.

---

## 3. Transfer Learning with ResNet18

The second model used **ResNet18**, a deep convolutional neural network that was originally trained on the **ImageNet** dataset.

Transfer learning was applied using the following steps:

1. The pretrained **ResNet18** model was loaded.
2. The convolutional layers were **frozen** so that their parameters would not be updated during training.
3. The final **fully connected layer** was replaced with a new layer matching the number of AQI classes.
4. Only this new classification layer was trained on the dataset.

This method allows the model to reuse general visual features learned from large datasets.

---

# Model Evaluation

Both models were evaluated using the **test dataset**. The following performance metrics were used:

- **Accuracy**
- **Precision**
- **Recall**
- **F1-score**

A **confusion matrix** was also generated to analyze the distribution of correct and incorrect predictions across AQI classes.

Additionally, training and validation curves were plotted to observe the learning behavior of the models across epochs.

---

# Results

| Model | Test Accuracy |
|------|------|
| CNN (trained from scratch) | **84.44%** |
| ResNet18 (Transfer Learning) | **71.33%** |

---

# Observations

Interestingly, the CNN trained from scratch achieved higher test accuracy compared to the pretrained ResNet18 model.

Although transfer learning often improves performance, this result can occur for several reasons:

- The dataset used in this experiment is relatively small.
- Features learned from ImageNet may not perfectly match visual patterns associated with air pollution.
- The custom CNN may have adapted more effectively to the specific characteristics of this dataset.

It was also observed that the CNN achieved strong training accuracy but showed mild signs of overfitting during training.

---

# Repository Contents

The project repository includes the following files:

- **AQI_Image_Classification.ipynb** – Google Colab notebook containing the full implementation  
- **data.csv** – dataset file containing image labels  
- **README.md** – description of the project and methodology

---

# Conclusion

This experiment explored two different approaches for predicting AQI categories from images: a CNN designed from scratch and a pretrained ResNet18 model using transfer learning.

While pretrained networks are generally advantageous due to their prior knowledge from large datasets, the results of this experiment showed that the custom CNN achieved slightly higher accuracy on the test dataset. This suggests that models trained directly on domain-specific data can sometimes capture task-specific visual patterns more effectively.

Overall, the experiment highlights how factors such as dataset size, feature relevance, and training configuration can significantly influence model performance.
