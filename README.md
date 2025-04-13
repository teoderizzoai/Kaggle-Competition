# 🏨 Expedia Hotel Booking Prediction (Kaggle Competition)

[![LightGBM](https://img.shields.io/badge/-LightGBM-006400?logo=lightgbm&logoColor=white&style=flat)](https://lightgbm.readthedocs.io/) 
[![Python](https://img.shields.io/badge/-Python-3776AB?logo=python&logoColor=white&style=flat)](https://www.python.org/)  

## 📘 Project Summary

This project was part of the "Data Mining Techniques" course at Vrije Universiteit Amsterdam. In a group of three, we participated in a Kaggle-style competition using Expedia's hotel booking data to build a ranking model that predicts which hotel a user is most likely to book.

We received a final grade of **9.5/10** for this project.

## 👋 What I Did 

As part of this project, I was responsible for:

- Cleaning and preprocessing over 5 million rows of hotel search and booking data
- Handling extensive missing values and outliers (especially in price and competitor features)
- Engineering advanced features based on user history, price differences, location desirability, and temporal components
- Implementing machine learning models using both classification and ranking approaches
- Fine-tuning hyperparameters and evaluating models using NDCG@5
- Creating a relevance scoring system for LambdaMART to better model real-world user behavior

---

## 🧠 Data Understanding

- 5 million+ entries in both training and test sets
- 50 features grouped into categories like hotel characteristics, user info, search query, and competition metrics
- Very high class imbalance: 95% of entries are negative (not clicked/booked)
- Significant missing data (up to 90%) in competitor and historical features

📈 **Key Insight:** Clicked results had a 62.4% chance of being booked — a valuable feature for modeling!


---

## 🧼 Data Preparation

- Imputed missing values using statistical strategies (zero, median, min, mean)
- Dropped unreliable fields (e.g. gross_booking_usd, site_id)
- Normalized skewed fields like price and star rating
- Engineered custom features:
  - `pricediff`, `reviewscorediff`, `stardiff`, `propscore1diff`, `propscore2diff`
  - `histpricediff`, `histstardiff`, `pricechange`

---

## 🤖 Modeling

### 📌 1. LGBM Classifier (baseline)
- Used `booking_bool` as target
- Performed grid search with cross-validation on 70/30 train-validation split
- Achieved local **NDCG@5 = 0.51**

### 📌 2. LambdaMART Ranker (final model)
- Converted problem into Learning-to-Rank using LightGBM ranker
- Assigned custom relevance scores: 5 = booked, 1 = clicked, 0 = ignored
- Handled group splits by search ID to avoid leakage
- Final training used 69 features and 3000 estimators

✅ **Best Score:** Kaggle leaderboard rank **#67** with score **0.38531**

---

## 📊 Key Takeaways

- Tree-based models (especially boosting) perform well on noisy, real-world data
- Proper feature engineering is crucial for Learning-to-Rank tasks
- Classification models can serve as baselines, but rankers better fit real-world use cases
- Data imbalance strategies like downsampling don’t always improve performance

---

## 🎓 Grade: **9.5 / 10**  
Course: *Data Mining Techniques — Vrije Universiteit Amsterdam*

<p align="center">Made with 💡 teamwork, ☕ debugging, and lots of Gradient Boosting 🌲</p>
