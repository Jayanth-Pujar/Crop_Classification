# Crop Classification Using Transfer Learning

## Project Overview

This project implements an image classification model to classify crop images into five categories:

- Maize
- Paddy
- Sugarcane
- Sunflower
- Wheat

The project uses TensorFlow/Keras and MobileNetV2 transfer learning for image classification.

## Dataset

The dataset contains manually collected crop images organized into five classes. To maintain a balanced dataset, 65 images were selected from each class.

| Dataset | Images |
|---|---:|
| Training | 230 |
| Validation | 50 |
| Testing | 45 |
| Total | 325 |

Images are resized to 224 × 224 pixels before being passed to the model.

## Data Preprocessing

The following preprocessing steps were used:

- Image resizing to 224 × 224
- MobileNetV2-compatible pixel preprocessing
- Data augmentation on training images
- Train/validation/test split
- Balanced number of images across all five classes

### Data Augmentation

Training images use random horizontal flipping, rotation, and zooming. Augmentation is applied during training to improve generalization and reduce overfitting.

## Model

### MobileNetV2 Transfer Learning

MobileNetV2 pretrained on ImageNet was selected as the base model. The original classification head was removed and a new classification head was added for the five crop classes.

```text
Input Image (224 × 224 × 3)
        ↓
Data Augmentation
        ↓
MobileNetV2 (ImageNet pretrained)
        ↓
Global Average Pooling
        ↓
Dense Layer (128, ReLU)
        ↓
Dropout (0.5)
        ↓
Dense Layer (5, Softmax)
        ↓
Crop Class Prediction
```

The pretrained MobileNetV2 layers were initially frozen and used for feature extraction.

## Training Configuration

| Parameter | Value |
|---|---|
| Model | MobileNetV2 |
| Input Size | 224 × 224 |
| Batch Size | 16 |
| Maximum Epochs | 30 |
| Optimizer | Adam |
| Learning Rate | 0.0001 |
| Loss Function | Sparse Categorical Crossentropy |
| Output Activation | Softmax |
| Number of Classes | 5 |
| Early Stopping | Yes |

Early stopping monitors validation loss and restores the best model weights.

## Evaluation

The model was evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- Training and validation accuracy
- Training and validation loss

### Test Result

**Test Accuracy: 68.89%**

The test set contains only 45 images, so the result should be interpreted with caution because each individual prediction has a relatively large effect on the reported accuracy.

The classification report and confusion matrix are included in the notebook.

## Analysis

The model performed best on the **Sunflower** class, while **Paddy** was one of the more difficult classes.

The confusion matrix showed errors between visually similar crop categories, particularly among Paddy, Wheat, Maize, and Sugarcane.

The relatively small dataset is an important limitation of this project.

## Possible Improvements

1. Collect more images for each crop class.
2. Increase image diversity in backgrounds, lighting, angles, and crop appearance.
3. Apply additional data augmentation techniques.
4. Fine-tune selected deeper layers of MobileNetV2 using a smaller learning rate.
5. Evaluate the model using a larger and more diverse test dataset.

## Prediction

A prediction function is included in the notebook. It accepts an image path and returns the predicted crop class and prediction confidence.

Example:

```text
Predicted Crop: Wheat
Confidence: 87.32%
```

## Project Structure

```text
Crop_Classification/
│
├── Crop_Classification.ipynb
├── README.md
└── requirements.txt
```

## Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Matplotlib
- Scikit-learn
- MobileNetV2
- Transfer Learning
- Computer Vision
