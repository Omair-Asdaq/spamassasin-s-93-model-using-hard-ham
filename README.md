# spamassasin-s-93-model-using-hard-ham
this model  is something thats quite easy to replicate and it can afford many improvements uses the public dataset from spamassasin

# Spam Detection Using Logistic Regression

This repository contains a Python-based spam detection model trained on the [SpamAssassin public corpus](http://spamassassin.apache.org/old/publiccorpus/). The model uses a **custom tokenization pipeline** with **CountVectorizer** and **Logistic Regression**, including,albeit not much, hyperparameter tuning to balance spam and ham classification.

---

## Dataset

- **Ham**: Emails classified as legitimate.
- **Spam**: Emails classified as spam.
- **Sources**: SpamAssassin public corpus (2003-02-28)  
  - Easy Ham: `20030228_easy_ham.tar.bz2`  
  - Hard Ham: `20030228_hard_ham.tar.bz2`  
  - Spam: `20030228_spam.tar.bz2`

**Note**: All datasets are extracted and processed locally. Only links are provided here.

---

## Preprocessing

- Converted all text to lowercase
- Removed special characters: `()[]{};:"`
- Replaced numbers with the token `NUMBER`
- Replaced URLs (including malformed URLs) with `URL`
- Custom tokenization that splits on whitespace, punctuation, and common separators
- Removed duplicate tokens per email

---

## Model

- **Classifier**: Logistic Regression
- **Features**: Bag-of-words using `CountVectorizer` with the global vocabulary
- **Hyperparameters**:
  - `C = 0.01` (strong regularization for better generalization)
  - `class_weight = 'balanced'` (to handle imbalanced spam vs ham)
- **Cross-validation**: Stratified 5-fold CV
- **Decision threshold**: Default 0.5 (can be adjusted for precision-recall tradeoff)

---

## Performance

### Cross-validation (Train set)
Cross-validation f1: [0.93793103 0.95238095 0.93793103 0.95104895 0.95833333]
Mean CV f1: 0.9475250611457507
Train Accuracy: 0.9771428571428571
              
              
              precision    recall  f1-score   support

           0       1.00      0.93      0.96       175
           1       0.97      1.00      0.98       350

    accuracy                           0.98       525
   macro avg       0.98      0.97      0.97       525
weighted avg       0.98      0.98      0.98       525

### Test set (Hard Ham + Spam)
Test Accuracy: 0.9333333333333333
             
              
              precision    recall  f1-score   support

           0       1.00      0.80      0.89        75
           1       0.91      1.00      0.95       150

    accuracy                           0.93       225
   macro avg       0.95      0.90      0.92       225
weighted avg       0.94      0.93      0.93       225


> The model is not that bad(still bad though)
