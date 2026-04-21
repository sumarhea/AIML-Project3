# Bank Marketing Classification Project

    This project builds and compares multiple machine learning models to predict whether a client will subscribe to a term deposit based on bank marketing data.

    The goal is to improve prediction performance using classification models and evaluate them using Accuracy, F1 Score, and Recall.

## Dataset

    •Source: Bank Marketing Dataset (bank-additional-full.csv) 
    •Records: ~41,000 customers 
    •Target variable: y (yes = 1, no = 0) 

## Features Used

    •age 
    •job 
    •marital 
    •education 
    •default 
    •housing 
    •loan 

## Data Preprocessing

    •Removed duration column (data leakage prevention) 
    •Encoded target variable (yes/no → 1/0) 
    •Handled missing-like values (pdays = 999 → -1) 
    •One-hot encoding for categorical variables 
    •Standard scaling for numerical features 
    •Train-test split (80/20, stratified) 

## Models Used

The following models were trained and tuned:

    •Logistic Regression 
    •K-Nearest Neighbors (KNN) 
    •Decision Tree Classifier 
    •Support Vector Machine (Linear SVC / SVC) 

## Hyperparameter Tuning

    GridSearchCV was used to optimize:
    •Logistic Regression: C, class_weight 
    •KNN: n_neighbors, weights 
    •Decision Tree: max_depth, min_samples_split, class_weight 
    •SVM: C, kernel, class_weight 

## Evaluation metric used during tuning

    •F1 Score 

## Model Evaluation Metrics

Models were evaluated using:

•Accuracy
•F1 Score (primary metric)
•Recall

### What your results mean

    1. Baseline Model is very strong
            Baseline Accuracy = 0.887 
            This means 88.7% of customers do NOT subscribe

            Important insight:
                The dataset is highly imbalanced

            So a “dumb model” that predicts no subscription for everyone already looks very accurate.
            That’s why accuracy alone is misleading.

    2. Why Accuracy is not useful here   
        Even your best ML models:
            •Logistic: 0.58 accuracy 
            •SVM: 0.60 accuracy 
            •Decision Tree: 0.69 accuracy 

            All are lower than baseline accuracy (0.887)
            This does NOT mean models are bad.
            It means:
                Accuracy is not the right metric for imbalanced classification

    3. Why F1 Score is the correct metric
        F1 balances:
            •Precision (avoid false positives) 
            •Recall (catch actual subscribers) 
        Your F1 results:
            Model F1 Score
            Decision Tree 0.262 (best)
            Logistic Regression	0.254
            SVM	0.251
            KNN	0.120
            Key takeaway:
                Decision Tree performs best when considering minority class detection.

    4. Best Model
        •Decision Tree (Tuned) is your best model 
        Why:
            Highest F1 score 
            Better recall than others 
            Captures more positive cases 

    5. Model Behavior Insight
        KNN is worst
        Very high accuracy (0.87) 
        But very low recall (0.07)
        Meaning:
            It almost never predicts “yes”, so it misses most real customers.

Logistic & SVM

    Balanced performance
    Better recall than tree in some cases
    But weaker overall separation

Decision Tree

Best trade-off

Slightly better at detecting minority class
