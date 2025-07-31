# DDoS Detection via Machine Learning Methodologies

## Non-Technical Explanation

This project develops an intelligent system to detect Distributed Denial-of-Service (DDoS) attacks in network traffic using machine learning. DDoS attacks are cyber threats where attackers flood a network with fake traffic to disrupt normal operations. Our system analyzes network flow data to automatically identify when such attacks are occurring, helping network administrators protect their systems. The model can distinguish between normal network traffic and 12 different types of DDoS attacks with high accuracy, providing an automated defense mechanism for network security.

## Data

**Dataset:** CIC-DDoS2019 dataset from the Canadian Institute for Cybersecurity (CIC) at the University of New Brunswick.

**Source:** [CIC-DDoS2019 Dataset](https://www.unb.ca/cic/datasets/ddos-2019.html)

**Dataset Characteristics:**

- **Size:** Two days of network activity data
- **Features:** 78 network flow features (77 after preprocessing)
- **Classes:** 13 classes (1 benign + 12 DDoS attack types)
- **Attack Types:** HTTP Flood, TCP Flood, UDP Flood, SYN Flood, ICMP Flood, Smurf Attack, HTTP Slowloris, HTTP Slow Read, LDAP, MSSQL, NetBIOS, Port Scan

**Data Collection:** The dataset was created in a controlled testbed environment with:

- Normal traffic from 25 profiled users (HTTP, HTTPS, FTP, SSH, email)
- Controlled replay of various DDoS attacks
- Network traffic captured as PCAP files
- Flow statistics extracted for machine learning analysis

**Preprocessing:** The data underwent extensive preprocessing including:

- Removal of duplicate values and missing data handling
- Feature selection (dropping single-value and highly correlated features)
- Categorical feature encoding
- Data normalization for numerical features

## Model

**Primary Model:** XGBoost (Extreme Gradient Boosting) classifier

**Model Selection Process:** We evaluated multiple machine learning algorithms:

- **XGBoost:** Best overall performance (F1 Score: 71.43%, Accuracy: 75.19%)
- **MLP Classifier:** Strong performance (F1 Score: 71.02%, Accuracy: 74.74%)
- **Random Forest:** Good performance but lower F1 score (64.63%)
- **Logistic Regression:** Baseline performance (65.12% F1)

**Why XGBoost:** XGBoost was chosen because it:

- Achieved the highest F1 score, indicating better balance between precision and recall
- Handles class imbalance well through its boosting mechanism
- Provides feature importance for interpretability
- Offers good generalization performance
- Supports multi-class classification effectively

**Model Architecture:**

- **Algorithm:** Gradient boosting with decision trees
- **Hyperparameters:** Learning rate=0.1, max_depth=6, n_estimators=200
- **Objective:** Multi-class classification
- **Regularization:** L1 and L2 regularization to prevent overfitting

## Hyperparameter Optimization

**Optimization Method:** Grid Search with 5-fold cross-validation

**Optimized Parameters:**

- **Learning Rate:** Tested values [0.01, 0.1, 0.2] - Best: 0.1
- **Max Depth:** Tested values [3, 6, 9] - Best: 6
- **Number of Estimators:** Tested values [100, 200, 300] - Best: 200

**Validation Strategy:**

- **Cross-validation:** 5-fold cross-validation for robust evaluation
- **Train/Test Split:** 70/30 split for final evaluation
- **Metrics:** F1 score as primary optimization metric due to class imbalance

**Results:** The optimized XGBoost model achieved:

- **Accuracy:** 75.19%
- **F1 Score:** 71.43%
- **ROC AUC:** 90.63%

## Results

**Performance Summary:**
Our XGBoost model successfully detects DDoS attacks with high accuracy and demonstrates strong discriminative ability. The ROC AUC of 90.63% indicates excellent separation between benign and malicious traffic patterns.

**Key Findings:**

1. **Effective Attack Detection:** The model can distinguish between normal traffic and various DDoS attack types with high confidence
2. **Class Imbalance Handling:** Despite imbalanced classes, the model maintains good performance across all attack types
3. **Feature Importance:** Network flow duration, packet counts, and byte statistics are among the most important features for detection
4. **Robust Performance:** Cross-validation results show consistent performance across different data splits

**Model Comparison:**
| Model | Accuracy | F1 Score | ROC AUC |
|-------|----------|----------|---------|
| **XGBoost** | **75.19%** | **71.43%** | **90.63%** |
| MLP Classifier | 74.74% | 71.02% | 90.27% |
| Random Forest | 74.08% | 64.63% | 90.63% |
| Logistic Regression | 73.45% | 65.12% | 89.87% |

**Practical Implications:**

- The model can be deployed in real-time network monitoring systems
- Provides automated DDoS detection with minimal false alarms
- Supports multiple attack type classification for targeted response
- Offers interpretable results through feature importance analysis

**Limitations and Future Work:**

- The model is trained on a static dataset and may need updates for evolving threats
- Performance may vary in different network environments
- Additional attack types could be incorporated for broader coverage
- Real-time deployment optimization may be needed for high-traffic networks

## Project Structure

```
├── Portfolio-Submission-DDOS-Detection.ipynb  # Main Jupyter notebook
├── data_sheet.md                              # Dataset documentation
├── model_card.md                              # Model documentation
├── README.md                                  # Project overview
└── data/                                      # Dataset directory containing Parquet optimized files to save on disk size
```

## Usage

**Prerequisites:**

- Python 3.7+
- Required packages: pandas, numpy, scikit-learn, xgboost, matplotlib, seaborn

**Running the Project:**

1. Clone the repository
2. Open and run the Jupyter notebook
3. Follow the analysis steps to reproduce the results

**Model Deployment:**
The trained XGBoost model can be deployed for real-time DDoS detection by:

- Loading the trained model
- Preprocessing incoming network flow data
- Making predictions on new traffic patterns
- Implementing alerting mechanisms for detected attacks

## Contact Details

Contact the Canadian Institute for Cybersecurity for dataset-related inquiries.

**Dataset Source:** [Canadian Institute for Cybersecurity](https://www.unb.ca/cic/datasets/ddos-2019.html)
