#  Prediction System using End-to-End MLOps Pipeline

### *(DVC • MLflow • Docker • AWS • CI/CD)*

[![MLOps](https://img.shields.io/badge/MLOps-End--to--End-blue)](https://github.com/)
[![Python](https://img.shields.io/badge/Python-3.10-green)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Modern%20API-teal)](https://fastapi.tiangolo.com/)
[![DVC](https://img.shields.io/badge/DVC-Data%20Versioning-brightgreen)](https://dvc.org/)
[![MLflow](https://img.shields.io/badge/MLflow-Experiment%20Tracking-orange)](https://mlflow.org/)
[![Docker](https://img.shields.io/badge/Docker-Containerization-blue)](https://www.docker.com/)
[![AWS](https://img.shields.io/badge/AWS-ECR%20%7C%20EC2%20%7C%20S3-yellow)](https://aws.amazon.com/)

---

## 📌 Executive Summary

A **production-grade Machine Learning system** that implements a complete **End-to-End MLOps pipeline** — from data ingestion to automated deployment on AWS.

> **💡 Why this matters:** Most ML projects stop at Jupyter notebooks. This one demonstrates **deployment-ready, scalable, and maintainable ML systems** that can actually ship to production.

---

## 🎯 Recruiter Highlights

| Area | What This Project Shows |
|------|------------------------|
| **System Design** | Complete ML lifecycle with modular components |
| **Cloud Expertise** | AWS (EC2, ECR, S3, IAM) + MongoDB Atlas |
| **DevOps Skills** | Docker, CI/CD, GitHub Actions, self-hosted runners |
| **ML Engineering** | DVC, MLflow, experiment tracking, model registry |
| **Production Readiness** | FastAPI, environment configs, error handling, logging |
| **Code Quality** | Modular architecture, type hints, config-driven design |

---

## 🏗️ System Architecture

```text
┌─────────────────────────────────────────────────────────────────────┐
│                         END-TO-END MLOPS PIPELINE                    │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  MongoDB ──▶ Data Ingestion ──▶ Data Validation                     │
│                    │                    │                            │
│                    ▼                    ▼                            │
│              Data Transformation ◀── Schema (YAML)                   │
│                    │                                                 │
│                    ▼                                                 │
│              Model Training ──▶ MLflow (Tracking)                    │
│                    │                                                 │
│                    ▼                                                 │
│              Model Evaluation ──▶ (Threshold: 2% improvement)        │
│                    │                                                 │
│                    ▼                                                 │
│              Model Pusher ──▶ AWS S3 (Model Registry)                │
│                    │                                                 │
│                    ▼                                                 │
│              FastAPI Prediction Pipeline                             │
│                    │                                                 │
│                    ▼                                                 │
│              Docker ──▶ ECR ──▶ EC2 ──▶ LIVE 🚀                      │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Technology Stack

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Language** | Python 3.10 | Core development |
| **Web Framework** | FastAPI | High-performance prediction API |
| **Data Processing** | Pandas, NumPy, Scikit-learn | EDA, transformations, modeling |
| **Database** | MongoDB Atlas | Scalable data storage |
| **Experiment Tracking** | MLflow | Parameter/metrics logging |
| **Data Versioning** | DVC | Reproducible data pipelines |
| **Containerization** | Docker | Environment consistency |
| **Cloud Storage** | AWS S3 | Model registry |
| **Container Registry** | AWS ECR | Docker image storage |
| **Compute** | AWS EC2 (t2.medium) | Production deployment |
| **CI/CD** | GitHub Actions + Self-hosted Runner | Automated deployment |
| **Security** | AWS IAM | Access management |

---

## 📁 Production-Ready Structure

```
Prediction-System-using-End-to-End-MLOps-Pipeline-DVC-MLflow-Docker/
│
├── src/                          # Core source code
│   ├── components/               # Pipeline components
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   ├── model_evaluation.py
│   │   └── model_pusher.py
│   │
│   ├── configuration/            # MongoDB & AWS connections
│   ├── constants/                # Global configuration
│   ├── entity/                   # Dataclasses (configs & artifacts)
│   ├── pipeline/                 # Training & prediction pipelines
│   ├── aws_storage/              # S3 interaction layer
│   └── utils/                    # Logging, exceptions, helpers
│
├── notebook/                     # EDA + MongoDB data upload
├── templates/                    # Web UI (minimal interface)
├── static/                       # CSS/assets
├── .github/workflows/            # CI/CD pipeline definition
├── Dockerfile                    # Container configuration
├── app.py                        # FastAPI application
├── requirements.txt              # Dependencies
├── setup.py                      # Local package installation
├── pyproject.toml                # Modern Python packaging
└── config.schema.yaml            # Data validation schema
```

---

## 🔄 Pipeline Components in Detail

### 1️⃣ Data Ingestion
- Connects to MongoDB Atlas using environment variables
- Fetches data, converts to DataFrame
- Creates ingestion artifacts for downstream components

### 2️⃣ Data Validation
- Validates against `config.schema.yaml`
- Checks data types, missing values, constraints
- Prevents bad data from entering pipeline

### 3️⃣ Data Transformation
- Feature engineering pipeline
- Preprocessing (scaling, encoding, imputation)
- Custom transformer classes in `estimator.py`

### 4️⃣ Model Training
- Trains multiple algorithms
- Hyperparameter tuning
- Logs everything to MLflow

### 5️⃣ Model Evaluation
- Compares new model against existing model from S3
- **2% improvement threshold** required for acceptance
- Prevents model degradation

### 6️⃣ Model Pusher
- Uploads accepted models to S3 bucket
- Maintains versioned model registry
- Production-ready model retrieval

### 7️⃣ Prediction Pipeline
- FastAPI endpoints for real-time predictions
- Loads latest model from S3
- Returns predictions in milliseconds

---

## ☁️ AWS Infrastructure

```text
┌──────────────────────────────────────────────────────────────┐
│                        AWS ARCHITECTURE                       │
├──────────────────────────────────────────────────────────────┤
│                                                               │
│   GitHub ──▶ GitHub Actions ──▶ Build ──▶ ECR                │
│                 │                      │                      │
│                 │                      ▼                      │
│                 │                 Docker Image                │
│                 │                      │                      │
│                 │                      ▼                      │
│                 └──────────────▶ EC2 (Self-hosted Runner)     │
│                                      │                         │
│                                      ▼                         │
│                              ┌──────────────┐                 │
│                              │  🚀 LIVE API  │                 │
│                              │  Port :5080   │                 │
│                              └──────────────┘                 │
│                                                               │
│   S3: my-model-mlopsproj/model-registry/                      │
│                                                               │
└──────────────────────────────────────────────────────────────┘
```

---

## 🐳 Docker Configuration

```dockerfile
# Multi-stage build for optimization
FROM python:3.10-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
EXPOSE 5080

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "5080"]
```

```bash
# Build and run
docker build -t vehicle-prediction .
docker run -p 5080:5080 vehicle-prediction
```

---

## 🔄 CI/CD Pipeline (GitHub Actions)

```yaml
# Trigger: push to main branch
name: Deploy to EC2

jobs:
  deploy:
    runs-on: self-hosted  # EC2 runner
    steps:
      - Checkout code
      - Build Docker image
      - Push to ECR
      - Pull and run on EC2
```

**Self-hosted runner setup on EC2:**
```bash
# EC2 instance (Ubuntu 24.04, t2.medium, 30GB)
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
# Configure GitHub self-hosted runner
./run.sh  # Runner connects to GitHub
```

---

## 🔐 Environment Configuration

### MongoDB Atlas
```bash
# Bash / Mac / Linux
export MONGODB_URL="mongodb+srv://<username>:<password>@cluster.mongodb.net/"

# Windows PowerShell
$env:MONGODB_URL = "mongodb+srv://<username>:<password>@cluster.mongodb.net/"
```

### AWS Credentials
```bash
export AWS_ACCESS_KEY_ID="AKIA..."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_DEFAULT_REGION="us-east-1"
```

### GitHub Secrets (for CI/CD)
```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
```

---

## 🌐 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/` | Web UI interface |
| `POST` | `/predict` | Real-time prediction |
| `GET` | `/training` | Trigger retraining pipeline |

### Sample Prediction Request
```bash
curl -X POST http://localhost:5080/predict \
  -H "Content-Type: application/json" \
  -d '{"feature1": 42, "feature2": 3.14}'
```

---

## 🚀 Deployment

**Live Application:**
```
http://<EC2-PUBLIC-IP>:5080
```

**Port Configuration:** EC2 security group inbound rule (Custom TCP, port 5080, 0.0.0.0/0)

---

## 📊 What This Demonstrates to Recruiters

| Skill | Evidence in Project |
|-------|---------------------|
| **MLOps** | Complete pipeline from ingestion → deployment |
| **Cloud** | AWS + MongoDB Atlas integration |
| **DevOps** | Docker, CI/CD, self-hosted runners |
| **Software Engineering** | Modular code, config-driven, error handling |
| **ML Best Practices** | DVC, MLflow, model registry, validation |
| **API Development** | FastAPI with prediction endpoints |
| **Security** | Environment variables, IAM, network configs |

---

## 📈 Future Enhancements

- [ ] **Monitoring:** Prometheus + Grafana for model performance
- [ ] **Explainability:** SHAP/LIME integration
- [ ] **Automated Retraining:** Scheduled pipeline triggers
- [ ] **A/B Testing:** Compare model versions in production
- [ ] **CI/CD Improvements:** Canary deployments

---

## 🧠 Key Takeaways from Building This

1. **Data versioning prevents silent failures** — DVC caught a data schema mismatch early
2. **Model registry in S3** simplifies rollbacks and A/B testing
3. **Self-hosted runners** reduce CI/CD costs and latency
4. **FastAPI async capabilities** handle concurrent prediction requests efficiently
5. **2% evaluation threshold** prevents accidental model degradation

---

## 📬 Connect

This project showcases **production-ready MLOps engineering**. For technical discussions or opportunities:

- **GitHub:** [https://github.com/sai-gajja]
- **LinkedIn:** [https://www.linkedin.com/in/sai-gajja/]

---

## ⭐ Support

If this project helps you understand MLOps best practices, consider giving it a ⭐ on GitHub.

---

**Built with:** Python • FastAPI • DVC • MLflow • Docker • AWS • MongoDB • GitHub Actions

---

