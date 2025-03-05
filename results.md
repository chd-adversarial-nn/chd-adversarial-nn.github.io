---
layout: single 
title: Mitigating Gender Bias in Coronary Heart Disease Prediction
permalink: /results
author_profile: true
classes: wide
toc: true
toc_label: Results & Beyond
toc_icon: "microscope"
header:
    overlay_image: /assets/images/header.jpg
---
## Baseline Model

| Metric | Score |
| --- | --- |
| Accuracy | 0.8789 | 
| Balanced Accuracy | 0.7181 |

Because there is such a large gap between the two metrics, we can infer that the model is struggling to make correct predictions for the minority class. This means the model might be overlooking CHD labeled patients and is showing bias towards predicting Non-CHD patients.

| Metric | Score |
| --- | --- | --- |
| Demographic Parity Difference | -0.1876 |
| Equal Opportunity Difference | -0.2409 |
| Disparate Impact | 0.466 | 

Keeping in mind that the ideal scores for Demographic Parity Difference and Equal Opportunity Difference should both be 0 and for Disparate Impact an ideal score of 1, we can conclude that the baseline model fails to provide equal representation between all groups within the sensitive classes.

## Adversarial Neural Network Model

The best configuration of hyperparameters we found was as follows:

| Learning Rate | Batch Size | Lambda | Adversarial Model Architecture |
| --- | --- | --- | --- |
| 0.001 | 32 | 0.05 | Logistic Regression |

With this model, we were able to achieve the following  metrics:

| Metric | Score |
| --- | --- |
| Accuracy | 0.7715  | 
| Balanced Accuracy | 0.7722 |

![Accuracy and Balanced Accuracy over Epochs](/assets/images/model_accuracies.png)
*Visuals: Progression of accuracy and balanced accuracy over epochs of training.*

Comparing these numbers to our baseline model, the test accuracy score dropped significantly from 0.8789 to 0.7715 but the test balanced accuracy increased from 0.7181 to 0.7715. This is likely due to the fact that the baseline model trained on an extremely unbalanced dataset, enabling a high accuracy just from predicting `false` for all patients and diagnosing them as not having CHD.

| Metric | Score |
| --- | --- | --- |
| Demographic Parity Difference | 0.2436 |
| Equal Opportunity Difference | 0.0106 |
| Disparate Impact | 1.4245 |

![Fairness Metrics over Epochs](/assets/images/model_fairness.png)
*Visuals: Progression of demographic parity difference, equal opportunity difference, and disparate impact over epochs of training*

Considering the ideal values for all three fairness metrics, the model demonstrated an increase in magnitude of demographic parity from -0.1876 to 0.2436, significant decrease in magnitude of equal opportunity from -0.2409 to 0.0106, and slight decrease in disparate impact from 0.466 (0.534 to ideal) to 1.4245 (0.4245 to ideal).

## Discussion & Analysis

Our implementation of an adversarial model was designed to decrease equal opportunity difference while maintaining reasonable performance. In this pursuit, we achieved a decrease in magnitude of 95.6% from -0.2409 to 0.0106. While our overall accuracy decreased marginally, our balanced accuracy increased a notable amount, indicating better performance with a more balanced dataset.

In our evaluation, we were able to successfully combine our neural network predictor with adversarial debiaising to protect a sensitive feature in our dataset. While overall accuracy decreased, we believe the tradeoff is worthwhile in order to improve fairness and minimize bias. Especially in the context of healthcare, where patients health and wellbeing are at stake, it is of vital importance to consider fairness.

Importantly, we note that our model should under no context be used to conclusively diagnose patients for CHD. It is absolutely **not** a sufficient substitute for professional diagnosis and treatment from a licensed physician. We believe the value of our model lies primarily in our advent of the adversarial neural network configuration, and secondly as an iterative improvement on existing models used to predict CHD.

## Limitations

Despite promising results, our model has some limitations.
- Firstly, this model is only capable of protecting one feature, in our case gender. For contexts where multiple classes should be protected, further development is required
- Another limitation is that this framework primarily focuses on a single fairness metric. While in our results changes in other fairness metrics are observed, those changes may not always occur
- Given our limited computational resources, our model would not have been able to accomodate for a larger dataset. Further research could leverage more powerful processors and improve model efficiency to potentially achieve better results

## Final Thoughts

In this project, we demonstrated that adversarial debiasing can significantly reduce gender bias in Coronary Heart Disease prediction while maintaining reasonable accuracy. Our approach achieved a reduction of 95.6% in magnitude of equal opportunity difference to ensure more equitable classification accuracy across genders.

This work addresses a critical need as AI and ML systems become increasingly prevalent in healthcare, where algorithmic biases can perpetuate or amplify existing disparities in treatment and outcomes. While our framework focused specifically on gender bias in CHD prediction, it offers a promising template that could be adapted to address other forms of demographic bias across various healthcare applications and beyond.

As AI/ML continues to transform healthcare delivery, our research contributes to the development of systems that are not only powerful and accurate but also fair and equitable for all patients.

Read More: [About Our Model](/project), [Our Development Process](/development)
