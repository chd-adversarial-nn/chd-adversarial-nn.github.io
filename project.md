---
layout: single 
title: Mitigating Gender Bias in Coronary Heart Disease Prediction
permalink: /project
header:
    image: /assets/images/header.jpg
---

*Note: You can replicate our project following our [setup instructions](/setup).*

In the rapidly evolving landscape of healthcare, Artificial Intelligence (AI) and Machine Learning (ML) are increasingly being employed to classify and diagnose patients. While these technologies offer immense potential, they also introduce significant challenges, particularly in the realm of bias and fairness. Our project focuses on a critical issue at the intersection of AI and healthcare: gender bias in the prediction of Coronary Heart Disease (CHD).

## Our Challenge

Coronary Heart Disease, a type of Cardiovascular Disease (CVD), has historically been associated with significant gender disparities in diagnosis and treatment. Often perceived as a "man's disease", female patients of CHD have experienced higher rates of misdiagnoses and suboptimal care. Our project aims to address this issue by developing an innovative machine learning model that can accurately and efficiently predict CHD while mitigating gender-based biases.

## Our Approach

We implement a neural network (NN) model using an adversarial configuration to tackle this challenge. Our approach involves:

1. A primary neural network model for CHD classification
2. A secondary "discriminator" model designed to detect and penalize gender-based biases

By leveraging this adversarial setup, we encourage our primary model to focus on relevant diagnostic features while discouraging reliance on sensitive attributes like gender. This methodology aims to promote more equitable healthcare outcomes, particularly for underrepresented patient populations in CHD diagnosis and treatment.

## Our Dataset

Our project utilizes health statistics data from the National Health and Nutrition Survey (NHANES), a comprehensive dataset that includes demographic, laboratory, and questionnaire data from over 37,000 individuals. We select and process 35 features to train our model, which can be referenced in our [complete list of features](/project/features).

## Project Goals

Through this project, we aim to:

1. Develop a fair and unbiased algorithm for CHD classification
2. Maintain clinically relevant accuracy while reducing gender-based disparities
3. Contribute to the growing body of literature on ethical AI use in healthcare
4. Offer a novel approach to mitigating demographic biases in cardiovascular disease diagnostics

We invite you to explore our website to learn more about our development process, methodologies, and the results of our research. Our work represents a step towards more equitable and accurate CHD prediction across all demographic groups, potentially improving healthcare outcomes for patients regardless of gender.

