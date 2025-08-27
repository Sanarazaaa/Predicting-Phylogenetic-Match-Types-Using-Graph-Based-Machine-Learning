# Predicting-Phylogenetic-Match-Types-Using-Graph-Based-Machine-Learning


## Project Summary
This project predicts the type of relationship between species in a phylogenetic dataset using a network-based machine learning approach. Species are represented as nodes in a graph, and edges correspond to observed matches. By combining network features (degree, betweenness, closeness) with species name similarity and genus information, a Random Forest classifier predicts edge types, handling class imbalance with SMOTE and balanced class weights. This approach demonstrates a unique intersection of phylogenetics, network analysis, and machine learning.

---

## Dataset
The dataset contains species pairs and their match types:

| Column      | Description |
|------------|-------------|
| `Species1` | First species in the pair |
| `Species3` | Second species in the pair |
| `Match.type` | Type of match between species (e.g., `1BL to 1BT`, `Many BL to 1BT`) |

- Rare classes with fewer than 3 samples are merged into `"Other"`.  
- The dataset is **imbalanced**, with the majority class (`1BL to 1BT`) dominating.

<img width="247" height="136" alt="image" src="https://github.com/user-attachments/assets/d66d5587-b7c7-4c8b-a4d2-4a19f9547abe" />

---

## Methodology

1. **Graph Construction**
   - Nodes = species  
   - Edges = species pairs with a match type label

2. **Feature Engineering**
   - Network features: degree, betweenness centrality, closeness centrality of each species  
   - String-based features: Levenshtein similarity of species names, same genus flag

3. **Handling Imbalanced Classes**
   - Merge extremely rare classes into `"Other"`  
   - Apply SMOTE oversampling on the training set  
   - Train Random Forest with `class_weight='balanced'`

4. **Model Training & Evaluation**
   - Stratified train-test split (80% train, 20% test)  
   - Random Forest classifier trained on resampled training data  
   - Evaluation metrics: precision, recall, F1-score  
   - Feature importance analyzed to understand key predictors

---


**Feature Importance:**
- `lev_sim` (string similarity): 0.242  
- `clos_v` (closeness centrality of node v): 0.227  
- `clos_u` (closeness centrality of node u): 0.202  
- `deg_u`, `deg_v`: 0.174, 0.105  
- `bet_u`, `bet_v`: 0.011, 0.002  
- `genus_same`: 0.038  

---

## Key Takeaways
- Achieves **high overall accuracy (~92%)**, though minority classes require attention.  
- String similarity and closeness centrality are the most predictive features.  
- Shows how **network analysis and ML** can complement phylogenetic studies.  

---

## Technologies
- Python 3  
- pandas, networkx, scikit-learn, imbalanced-learn  
- Levenshtein for string similarity  




