# Model Card for DDoS Detection Model

## Model Description

**Model Name:** XGBoost DDoS Detection Classifier

**Model Type:** Gradient Boosting Classification Model

**Input:**

- **Feature Count:** 77 preprocessed network flow features (after feature selection)
- **Feature Types:**
  - 20 categorical features (encoded)
  - 57 numerical features (normalized)
- **Input Format:** Network flow statistics including packet counts, byte counts, flow duration, protocol information, and various statistical measures

**Output:**

- **Task:** Multi-class classification
- **Classes:** 13 classes (1 benign + 12 DDoS attack types)
- **Output Format:** Probability scores for each class
- **Prediction:** Class label with highest probability

**Model Architecture:**

- **Algorithm:** XGBoost (Extreme Gradient Boosting)
- **Base Learners:** Decision trees
- **Ensemble Method:** Gradient boosting with regularization
- **Hyperparameters:**
  - Learning rate: 0.1
  - Max depth: 6
  - Number of estimators: 200
  - Objective: Multi-class classification

## Performance

**Evaluation Metrics:**

- **Accuracy:** 75.19%
- **F1 Score:** 71.43%
- **ROC AUC:** 90.63%

**Model Comparison Results:**
| Model | Accuracy | F1 Score | ROC AUC |
|-------|----------|----------|---------|
| XGBoost | 75.19% | 71.43% | 90.63% |
| Random Forest | 74.08% | 64.63% | 90.63% |
| MLP Classifier | 74.74% | 71.02% | 90.27% |
| Logistic Regression | 73.45% | 65.12% | 89.87% |

**Performance Analysis:**

- XGBoost achieved the best overall performance across all metrics
- The model shows strong discriminative ability with ROC AUC of 90.63%
- F1 score of 71.43% indicates good balance between precision and recall despite class imbalance
- The model performs well in distinguishing between benign traffic and various DDoS attack types

**Evaluation Data:**

- **Test Set:** 30% of the CIC-DDoS2019 dataset
- **Cross-validation:** 5-fold cross-validation used for hyperparameter tuning
- **Evaluation Method:** Standard classification metrics on held-out test set

## Limitations

**Data Limitations:**

- **Class Imbalance:** The dataset contains imbalanced classes, with some attack types having fewer samples
- **Static Dataset:** The model is trained on a static dataset and may not capture evolving attack patterns
- **Limited Attack Types:** Only 12 DDoS attack types are represented, not covering all possible attack variations

**Model Limitations:**

- **Feature Dependence:** Performance depends heavily on the quality and relevance of extracted network flow features
- **Computational Cost:** XGBoost can be computationally intensive for real-time applications
- **Interpretability:** While feature importance is available, the model's decision process is not fully interpretable
- **Generalization:** Performance may degrade in network environments significantly different from the training data

**Operational Limitations:**

- **False Positives:** May generate false alarms for legitimate traffic patterns
- **False Negatives:** May miss novel or sophisticated DDoS attacks
- **Latency:** Real-time prediction may introduce processing delays
- **Scalability:** Performance may degrade with very high traffic volumes

## Trade-offs

**Performance vs. Interpretability:**

- **Trade-off:** XGBoost provides high performance but limited interpretability compared to simpler models
- **Mitigation:** Feature importance analysis and SHAP explanations are used to provide some interpretability

**Accuracy vs. Speed:**

- **Trade-off:** Higher accuracy comes with increased computational complexity
- **Mitigation:** Model can be optimized for speed by reducing tree depth or number of estimators

**Precision vs. Recall:**

- **Trade-off:** Optimizing for precision may reduce recall and vice versa
- **Current Balance:** F1 score of 71.43% indicates a reasonable balance between precision and recall

**Generalization vs. Specialization:**

- **Trade-off:** Model trained on specific attack types may not generalize to novel attacks
- **Mitigation:** Regular model updates and retraining with new data can help maintain performance

**False Positives vs. False Negatives:**

- **Trade-off:** Reducing false positives may increase false negatives and vice versa
- **Context:** In DDoS detection, false negatives (missing attacks) are typically more critical than false positives

## Model Training

**Training Data:**

- **Source:** CIC-DDoS2019 dataset
- **Size:** 70% of the dataset used for training
- **Preprocessing:** Feature scaling, encoding, and selection applied

**Hyperparameter Optimization:**

- **Method:** Grid Search with 5-fold cross-validation
- **Optimized Parameters:** Learning rate, max depth, number of estimators
- **Best Configuration:** Learning rate=0.1, max_depth=6, n_estimators=200

**Training Process:**

- **Validation:** 5-fold cross-validation
- **Early Stopping:** Not used (fixed number of estimators)
- **Regularization:** L1 and L2 regularization included in XGBoost

## Deployment Considerations

**System Requirements:**

- **Memory:** Sufficient RAM for model loading and inference
- **Processing:** CPU or GPU support for XGBoost
- **Storage:** Model file size approximately 50-100 MB

**Integration:**

- **API:** RESTful API for real-time predictions
- **Batch Processing:** Support for batch prediction on historical data
- **Monitoring:** Performance monitoring and alerting systems

**Maintenance:**

- **Regular Updates:** Model should be retrained periodically with new data
- **Performance Monitoring:** Continuous monitoring of prediction accuracy
- **Feature Drift:** Monitoring for changes in input feature distributions
