---
layout: single
title: Development Process 
permalink: /development
classes: wide
author_profile: true
toc: true
toc_label: "Development Process"
toc_icon: "terminal"
header:
    overlay_image: /assets/images/header.jpg
---
## 1. Literature Review and Background Research

Our project began with a review of existing literature to understand:

- The state of CHD diagnosis and treatment, particularly concerning gender disparities
- The application of AI/ML within healthcare, with an emphasis on cardiovascular disease
- Methodologies for identifying and mitigating bias in AI systems

A full list of references is available on our [works cited page](/references). Notably, [Dutta et. al. (2020)](http://dx.doi.org/10.1016/j.eswa.2020.113408)'s Convolutional Neural Network model demonstrated the potential for Neural Networks in predicting CHD and served as a key reference in our initial model development plans.

## 2. Data Acquisition and Preprocessing

We utilized data from the [National Health and Nutrition Examination Survey (NHANES)](https://www.cdc.gov/nchs/nhanes/about/), a comprehensive survey conducted by the CDC's National Center for Health Statistics. Our data processing involved:

- Accessing NHANES data via the public API, compiling information across multiple years (1999-2016)
- Addressing inconsistencies in variable naming conventions and data formatting across different survey periods
- Managing missing data; we chose to remove observations with many null values and impute mean value where reasonable, resulting in a final dataset of over 30,000 observations
- Selecting 35 key variables relevant to CHD prediction (see our [list of features](/project/features))

## 3. Baseline Model Development

Prior to developing our primary model, we established performance baselines using the following algorithms:

- Random Forest
- Logistic Regression
- Simple Neural Network

These models were evaluated based on both predictive accuracy and fairness metrics. Logistic Regression provided the most promising baseline, balancing performance and interpretability.

*Performance and fairness metrics for baseline and final models are presented on our [Results & Beyond](/results) page.*

## 4. Primary Model Design and Implementation

Our primary model is a Feed-Forward Neural Network implemented in TensorFlow. The architecture is as follows:

| Layer | Configuration |
| --- | --- |
| Input Layer | 35 units (corresponding to our selected variables) |
| Dense Layer | 32 units, ReLU activation |
| Dropout Layer | 30% dropout rate for regularization |
| Dense Layer | 16 units, ReLU activation |
| Output Layer | 1 unit, sigmoid activation (binary classification) |

We trained our model using Binary Cross-Entropy loss and the Adam optimizer. Evaluation metrics included Binary Accuracy and Balanced Accuracy. During each Epoch, our model is trained as follows:
1. Neural Network makes a Forward Pass on a batch
2. Neural Network Computes Loss (Binary Entropy Loss)
3. SGD Classifier uses NN prediction probabilities to predict sensitive attribute
4. Compute Binary Entropy Loss of Adversarial Model
5. Compute Combined Loss Function
6. Compute Gradients with Combined Loss
7. Update Weights with new gradients

We evaluated our model's predictive performance using accuracy, precision, recall, and F1 score. We evaluated our model's fairness using Demographic Parity Difference, Equal Opportunity Difference, and Disparate Impact.

## 5. Adversarial Debiaising

To directly address gender bias, we integrated an adversarial component into our model. This component aims to penalize the primary model for making predictions that heavily correlate with gender. Our adversarial model is an SGD Classifier trained to predict gender based on the primary model's predictions. By optimizing the primary model to minimize the adversarial model's accuracy, we encourage it to rely less on gender as a predictive factor.

![Visualizations of Accuracy, Primary Loss, Adversarial Loss over Epochs](/assets/images/model_loss.png)
*Visuals: Progression of accuracy, primary model loss, and adversarial model loss over epochs of training.*

As the combined model is trained, the primary model's loss decreases and the overall accuracy increases. Conversely, the the adversarial model's loss increases, representing a diminishing ability of the adversarial model to predict the protected feature from the primary model. In effect, the combined model becomes better at accurately predicting CHD while simultaneously becoming less biased in predicting based on gender as training progresses.

## 6. Hyperparameter Tuning and Optimization

We experimented with a series of hyperparameters to optimize model performance and fairness. Key hyperparameters included:

- Learning rate
- Batch size
- Lambda (trade-off parameter balancing accuracy and fairness)
- Adversarial model architecture (perceptron, SVM, logistic regression)

We systematically evaluated different hyperparameter combinations to identify the configuration that yielded the best overall results.

*Performance and fairness metrics for baseline and final models are presented on our [Results & Beyond](/results) page.*

Read More: [About Our Model](/project), [Results & Beyond](/results)
