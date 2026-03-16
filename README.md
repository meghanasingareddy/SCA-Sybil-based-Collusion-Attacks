# SCA — Sybil-based Collusion Attacks Detection in IIoT Federated Learning

A Django-based web application that detects **Sybil-based Collusion Attacks (SCA)** targeting **Industrial Internet of Things (IIoT)** data poisoning in **Federated Learning** environments.

> **Reference Paper:** *IEEE Transactions on Industrial Informatics* — Issue Date: 03 May 2022

---

## 📌 Overview

Federated Learning (FL) enables decentralized model training across IIoT devices without sharing raw data. However, FL is vulnerable to **Sybil-based collusion attacks**, where adversaries inject malicious nodes that collude to poison model updates through **label-flipping attacks**, degrading global model performance.

This project implements a web-based detection system that:

- Analyzes network traffic data from IIoT nodes to identify potential Sybil-based collusion attacks.
- Trains and compares multiple machine learning classifiers to detect attack patterns.
- Provides role-based functionality for **Remote Users** (data submission & prediction) and **Service Providers** (model training & monitoring).

---

## 🏗️ Architecture

```
SCA_Sybil_based_Collusion_Attacks/
├── Database/                          # MySQL database schema
│   └── sca_sybil_based_collusion_attacks.sql
├── sca_sybil_based_collusion_attacks/ # Django project root
│   ├── manage.py
│   ├── Network_Datasets.csv           # Training dataset
│   ├── Results.csv                    # Prediction results
│   ├── Remote_User/                   # Remote User app
│   │   ├── models.py                  # Data models
│   │   ├── views.py                   # User views & prediction logic
│   │   └── forms.py                   # User forms
│   ├── Service_Provider/              # Service Provider app
│   │   └── views.py                   # Admin views & ML training
│   ├── Template/                      # HTML templates & static files
│   │   ├── htmls/
│   │   │   ├── RUser/                 # Remote User templates
│   │   │   └── SProvider/             # Service Provider templates
│   │   └── images/                    # Static images
│   └── sca_sybil_based_collusion_attacks/
│       ├── settings.py                # Django settings
│       ├── urls.py                    # URL routing
│       └── wsgi.py                    # WSGI config
└── Datastructure.txt                  # Data field descriptions
```

---

## ✨ Features

### 🔐 Remote User Module
- **User Registration & Login** — Secure account creation and authentication.
- **Profile Management** — View and manage user profile details.
- **Attack Prediction** — Submit network traffic parameters (source/destination IP, ports, flags, ASN, packet/byte counts) and receive real-time attack detection predictions using an ensemble classifier.

### 🛡️ Service Provider Module
- **Admin Dashboard** — View registered remote users and manage the system.
- **ML Model Training** — Train and evaluate multiple classifiers on the network dataset:
  - Naive Bayes
  - Support Vector Machine (SVM)
  - Logistic Regression
  - Decision Tree Classifier
  - SGD Classifier
- **Attack Status Monitoring** — View all detected Sybil-based collusion attack statuses.
- **Detection Ratio Analysis** — Visualize the ratio of attacked vs. non-attacked network traffic.
- **Accuracy Comparison Charts** — Interactive charts comparing classifier accuracies.
- **Dataset Export** — Download predicted datasets as Excel files.

---

## 🧠 Machine Learning Pipeline

| Step | Description |
|------|-------------|
| **Data Ingestion** | Load `Network_Datasets.csv` with labeled network traffic data |
| **Feature Extraction** | Convert `Network_Node_Text` into numerical features using `CountVectorizer` |
| **Label Encoding** | Map labels — `0` → No Attack Found, `1` → Attack Found |
| **Train/Test Split** | 80/20 split for training and evaluation |
| **Model Training** | Train Naive Bayes, SVM, Logistic Regression, Decision Tree, and SGD classifiers |
| **Ensemble Prediction** | Use `VotingClassifier` (SVM + SGD) for final attack prediction |
| **Evaluation** | Accuracy score, confusion matrix, and classification report for each model |

---

## 🔧 Tech Stack

| Component | Technology |
|-----------|------------|
| **Backend** | Django 3.x (Python) |
| **Database** | MySQL |
| **ML Libraries** | scikit-learn, pandas |
| **Frontend** | HTML, CSS, JavaScript |
| **Data Export** | xlwt (Excel) |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.7+
- MySQL Server
- pip

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/meghanasingareddy/SCA-Sybil-based-Collusion-Attacks.git
   cd SCA-Sybil-based-Collusion-Attacks/SCA_Sybil_based_Collusion_Attacks
   ```

2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install django mysqlclient scikit-learn pandas xlwt
   ```

4. **Set up the MySQL database**
   - Create a database named `sca_sybil_based_collusion_attacks`.
   - Import the schema:
     ```bash
     mysql -u root -p sca_sybil_based_collusion_attacks < Database/sca_sybil_based_collusion_attacks.sql
     ```
   - Update `settings.py` with your MySQL credentials if needed.

5. **Run migrations**
   ```bash
   cd sca_sybil_based_collusion_attacks
   python manage.py migrate
   ```

6. **Start the development server**
   ```bash
   python manage.py runserver
   ```

7. **Access the application**
   - Home Page: [http://127.0.0.1:8000/](http://127.0.0.1:8000/)
   - Service Provider Login: [http://127.0.0.1:8000/serviceproviderlogin/](http://127.0.0.1:8000/serviceproviderlogin/)
     - Username: `Admin` | Password: `Admin`

---

## 📊 Dataset

The project uses `Network_Datasets.csv` containing network traffic features:

| Field | Description |
|-------|-------------|
| `source_ip` | Source IP address |
| `destination_ip` | Destination IP address |
| `start_time` | Timestamp of network activity |
| `Network_Node_Text` | Textual representation of network node activity |
| `source_port` | Source port number |
| `destination_port` | Destination port number |
| `flags` | Network flags |
| `site` | Network site identifier |
| `asn` | Autonomous System Number |
| `num_packets` | Number of packets transmitted |
| `num_bytes` | Number of bytes transmitted |
| `Label` | Attack label — `0` (No Attack) / `1` (Attack) |

---

## 🔑 Keywords

`IIoT` · `Federated Learning` · `Label Flipping Attacks` · `Sybil Attacks` · `Collusion Attacks` · `Network Security` · `Machine Learning` · `Django`

---

## 📄 License

This project is for academic and research purposes.
