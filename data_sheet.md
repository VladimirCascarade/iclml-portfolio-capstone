# Datasheet for CIC-DDoS2019 Dataset

## Motivation

**Purpose:** The CIC-DDoS2019 dataset was created to provide a comprehensive benchmark for evaluating machine learning-based DDoS (Distributed Denial-of-Service) attack detection systems. The dataset aims to address the limitations of existing datasets by providing realistic network traffic data that includes both benign traffic and various types of DDoS attacks.

**Creators:** The dataset was created by the Canadian Institute for Cybersecurity (CIC) at the University of New Brunswick, Canada.

**Funding:** The dataset was developed as part of academic research initiatives at the Canadian Institute for Cybersecurity.

## Composition

**Data Representation:** The dataset contains network flow statistics representing network traffic patterns. Each instance represents a network flow with extracted statistical features.

**Dataset Size:** The dataset contains network activity recorded over two days, including:

- Benign traffic from 25 profiled users engaging in normal activities (HTTP, HTTPS, FTP, SSH, email)
- Twelve different types of DDoS attacks
- More than 80 flow-based features extracted from PCAP files

**Attack Types Included:**

- **Application Layer Attacks:** HTTP Flood, HTTP Slowloris, HTTP Slow Read
- **Transport Layer Attacks:** TCP Flood, UDP Flood, SYN Flood
- **Network Layer Attacks:** ICMP Flood, Smurf Attack
- **Other Attacks:** LDAP, MSSQL, NetBIOS, Port Scan

**Missing Data:** The dataset has been preprocessed to handle missing values and ensure data quality. Some features may contain missing values that are handled during the preprocessing stage.

**Confidentiality:** The dataset contains network traffic data that was collected in a controlled testbed environment. While it represents real network patterns, it does not contain sensitive personal information or actual user communications.

## Collection Process

**Data Acquisition:** The data was collected using a controlled testbed environment where:

1. Normal user activities were simulated by 25 profiled users
2. DDoS attacks were replayed in a controlled manner
3. Network traffic was captured as PCAP (Packet Capture) files
4. Flow statistics were extracted from the captured packets

**Sampling Strategy:** The dataset represents a comprehensive sample of network traffic patterns rather than a random sample. It includes both normal traffic patterns and various attack scenarios to provide a balanced representation for machine learning applications.

**Time Frame:** The data was collected over a two-day period, providing sufficient temporal coverage to capture various network behaviors and attack patterns.

## Preprocessing/Cleaning/Labeling

**Preprocessing Steps:**

1. **Feature Extraction:** More than 80 flow-based features were extracted from PCAP files
2. **Data Cleaning:** Removal of duplicate values and handling of missing data
3. **Feature Selection:** Dropping of single-value features and highly correlated columns (correlation coefficient > 0.8) to minimize multicollinearity
4. **Label Encoding:** Categorical features were encoded for machine learning compatibility
5. **Data Balancing:** The dataset contains imbalanced classes, which is addressed during model training

**Raw Data Preservation:** The original PCAP files and raw flow statistics are preserved alongside the preprocessed dataset to support future research and validation.

## Uses

**Intended Applications:**

- DDoS attack detection and classification
- Network security monitoring systems
- Machine learning model development for cybersecurity
- Academic research in network security
- Benchmarking of intrusion detection systems

**Potential Limitations:**

- The dataset may not represent all possible DDoS attack variations
- Network environments may differ from the controlled testbed
- The dataset is static and may not reflect evolving attack patterns
- Class imbalance may affect model performance on minority attack types

**Risk Mitigation:**

- Users should validate models on their specific network environments
- Consider ensemble methods to handle class imbalance
- Regular model updates may be necessary for evolving threats
- Cross-validation should be used to ensure robust performance

**Inappropriate Uses:**

- The dataset should not be used as the sole basis for production security systems without additional validation
- Direct deployment without adaptation to specific network environments
- Use in environments with significantly different traffic patterns

## Distribution

**Distribution Method:** The dataset is publicly available through the Canadian Institute for Cybersecurity website at https://www.unb.ca/cic/datasets/ddos-2019.html

**Licensing:** The dataset is provided for academic and research purposes. Users should refer to the CIC website for specific terms of use and licensing information.

**Intellectual Property:** The dataset is subject to the intellectual property rights of the Canadian Institute for Cybersecurity. Users should comply with the stated terms of use.

## Maintenance

**Maintenance Responsibility:** The Canadian Institute for Cybersecurity at the University of New Brunswick maintains the dataset and provides updates and support.

**Contact Information:** For questions regarding the dataset, users can contact the Canadian Institute for Cybersecurity through their official website.

**Version Control:** The dataset version used in this project is the CIC-DDoS2019 release, which represents the current standard version for DDoS detection research.
