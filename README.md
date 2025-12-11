# NeuroShield

**AI-powered Behavioral Anomaly Detection System for Insider Threat Detection**

*Built for Microsoft Imagine Cup 2026 - Cybersecurity Category*

## 📋 Project Overview

NeuroShield is a cutting-edge behavioral anomaly detection platform that identifies insider threats in real-time using multi-agent AI orchestration. Organizations lose **$15B annually** to insider threats (data theft, sabotage, espionage). Traditional rule-based systems miss sophisticated behavioral anomalies. NeuroShield learns organizational culture patterns and detects deviations with AI-powered agents.

### Problem Statement
- ❌ Rule-based security systems miss sophisticated insider threats
- ❌ Reactive incident response (average dwell time: 207 days)
- ❌ No context-aware anomaly detection for organizational culture
- ❌ Manual correlation of multi-source security signals

### Our Solution
- ✅ ML-powered behavioral baseline learning (per user, role, time)
- ✅ Real-time anomaly detection across 7+ data sources
- ✅ Multi-agent orchestration for threat correlation
- ✅ Explainable AI with SHAP values
- ✅ <100ms inference latency
- ✅ Enterprise-grade scalability (1M+ events/sec)

## 🏗️ Architecture Overview

```
Data Ingestion → Stream Processing → Feature Engineering → Multi-Agent ML
    ↓                                                         ↓
Event Hubs     Stream Analytics    Azure ML Service    Risk Scoring Agent
(7+ sources)   (Real-time)         (PyTorch, XGBoost)  (Threat Correlation)
                                                         ↓
                                                    Alert & Response
                                                    (Dashboards, APIs)
```

## 📦 Tech Stack

### Core ML/AI
- **Python 3.10+** - Core development language
- **PyTorch** - Deep learning (Graph Neural Networks)
- **Scikit-learn** - Classical ML (Isolation Forest, XGBoost, Random Forest)
- **SHAP** - Model explainability
- **Pandas/NumPy** - Data processing

### Cloud & Infrastructure
- **Azure Event Hubs** - Real-time data ingestion (1M+ events/sec)
- **Azure Stream Analytics** - Real-time feature engineering
- **Azure Machine Learning** - ML pipelines, model registry, inference endpoints
- **Azure Cosmos DB** - User profiles, baselines (NoSQL)
- **Azure Synapse** - Data warehouse (historical analysis)
- **Azure Container Registry** - Docker image management
- **Azure Kubernetes Service (AKS)** - Inference & API scaling

### Backend & API
- **FastAPI** - Async REST API with auto-documentation
- **Redis** - Caching & rate limiting
- **PostgreSQL** - Transactional data
- **Docker** - Containerization

### Frontend
- **React + TypeScript** - Web dashboard
- **D3.js / Plotly** - Data visualizations & graphs
- **Material-UI** - Component library
- **Vercel** - Deployment

### DevOps & Monitoring
- **GitHub Actions** - CI/CD pipelines
- **Terraform** - Infrastructure as Code
- **Azure Application Insights** - Monitoring & APM
- **Kubernetes** - Orchestration & scaling

## 🚀 Getting Started

### Prerequisites
- Python 3.10+
- Docker & Docker Compose
- Git
- Azure CLI (for cloud deployments)
- Node.js 16+ (for frontend)

### Local Development Setup

```bash
# Clone the repository
git clone https://github.com/dipayansardar73-decode/NeuroShield.git
cd NeuroShield

# Create Python virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install -r requirements-dev.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your Azure credentials

# Start Docker services (Event Hubs, Cosmos DB, etc.)
docker-compose up -d

# Run tests
pytest tests/

# Start development servers
# Terminal 1: Backend API
python -m uvicorn api.main:app --reload

# Terminal 2: Feature engineering service
python services/feature_engineering/main.py

# Terminal 3: Model inference service
python services/inference/main.py

# Terminal 4: Frontend (from frontend/ directory)
npm install && npm start
```

## 📁 Project Structure

```
NeuroShield/
├── data/                          # Data ingestion & processing
│   ├── connectors/                # Log source connectors
│   │   ├── windows_eventlog.py
│   │   ├── network_logs.py
│   │   ├── email_metadata.py
│   │   └── base_connector.py
│   ├── parsers/                   # Log format parsers
│   ├── validators/                # Data quality checks
│   └── generators/                # Synthetic data for testing
│
├── ml/                            # Machine Learning pipeline
│   ├── features/                  # Feature engineering
│   │   ├── statistical.py
│   │   ├── temporal.py
│   │   ├── graph.py
│   │   └── feature_store.py
│   ├── models/                    # Model implementations
│   │   ├── baseline_models.py     # Isolation Forest, LOF, SVM
│   │   ├── supervised_models.py   # XGBoost, Random Forest
│   │   ├── gnn_model.py           # Graph Neural Network
│   │   └── ensemble.py            # Model ensemble
│   ├── training/                  # Training pipelines
│   │   ├── pipelines.py
│   │   ├── evaluation.py
│   │   └── hyperparameter_tuning.py
│   └── inference/                 # Real-time inference
│       ├── predictor.py
│       └── explainability.py
│
├── services/                      # Microservices
│   ├── feature_engineering/       # Real-time feature computation
│   ├── inference/                 # Real-time ML inference
│   ├── alert_orchestration/       # Multi-agent orchestration
│   └── response_automation/       # Automated response playbooks
│
├── api/                           # FastAPI backend
│   ├── main.py
│   ├── routes/
│   │   ├── predictions.py
│   │   ├── alerts.py
│   │   ├── baselines.py
│   │   └── admin.py
│   ├── middleware/                # Auth, logging, monitoring
│   └── models/                    # Pydantic schemas
│
├── frontend/                      # React dashboard
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── stores/                # Redux/Zustand state
│   │   └── App.tsx
│   └── package.json
│
├── azure/                         # Azure ML & Infrastructure
│   ├── ml_pipelines/              # Azure ML pipeline definitions
│   ├── terraform/                 # Infrastructure as Code
│   └── kubernetes/                # K8s manifests
│
├── tests/                         # Comprehensive test suite
│   ├── unit/
│   ├── integration/
│   └── e2e/
│
├── notebooks/                     # Jupyter notebooks for EDA
│   ├── 01_exploratory_data_analysis.ipynb
│   ├── 02_model_comparison.ipynb
│   └── 03_feature_importance.ipynb
│
├── docs/                          # Documentation
│   ├── ARCHITECTURE.md
│   ├── API_REFERENCE.md
│   ├── DEPLOYMENT.md
│   └── CONTRIBUTING.md
│
├── .github/
│   └── workflows/                 # GitHub Actions CI/CD
│       ├── test.yml
│       ├── build.yml
│       └── deploy.yml
│
├── docker-compose.yml             # Local development services
├── Dockerfile                     # Container image
├── requirements.txt               # Python dependencies
├── requirements-dev.txt           # Development dependencies
├── .env.example                   # Environment variables template
├── .gitignore
└── README.md
```

## 🔑 Key Features

### 1. **Multi-Source Data Ingestion**
- Windows Event Logs, Network/Proxy Logs, VPN Access
- Email Metadata, File Access Events, Endpoint Telemetry
- Cloud Activity (Azure, AWS), DNS Queries
- Real-time streaming via Azure Event Hubs

### 2. **Behavioral Baseline Learning**
- Per-user baselines (normal activity patterns)
- Role-based expectations
- Time-of-day and day-of-week seasonality
- Privilege escalation path mapping

### 3. **Anomaly Detection Ensemble**
- **Unsupervised**: Isolation Forest, Local Outlier Factor, One-Class SVM
- **Supervised**: XGBoost, Random Forest, LightGBM (with SHAP explainability)
- **Deep Learning**: Graph Neural Networks for relationship anomalies
- **Weighted Voting Ensemble** for robust predictions

### 4. **Multi-Agent Orchestration**
- **Behavior Analysis Agent** - Detects individual user anomalies
- **Risk Scoring Agent** - Quantifies threat severity
- **Threat Correlation Agent** - Links related incidents
- **Response Agent** - Recommends/executes response playbooks

### 5. **Real-Time Alerting**
- Dashboard with risk scorecards
- WebSocket streaming of live alerts
- Integration with Slack, Teams, SIEM systems
- Alert triage and feedback loop

### 6. **Explainability & Transparency**
- SHAP feature importance rankings
- Decision path visualization
- Model confidence scores
- Audit trail of all predictions

## 📊 Performance Targets

| Metric | Target |
|--------|--------|
| Detection Latency | <100ms (p95) |
| Throughput | 1M+ events/sec |
| Model AUC | >90% |
| Precision @ 10% False Positive Rate | >80% |
| Recall @ 10% False Positive Rate | >70% |
| Inference Cost | <$0.001 per prediction |

## 🔄 Development Roadmap

### Phase 1: Foundation (Weeks 1-2)
- [ ] GitHub repo setup & CI/CD skeleton
- [ ] Data ingestion framework (3+ connectors)
- [ ] Schema validation & data quality checks

### Phase 2: ML Pipeline (Weeks 3-5)
- [ ] Feature engineering (50+ features)
- [ ] Synthetic dataset creation (~10K labeled events)
- [ ] 7+ models trained (Isolation Forest → GNN)
- [ ] Ensemble model with >90% AUC

### Phase 3: Azure ML & Backend (Weeks 5-7)
- [ ] Azure ML pipelines & model registry
- [ ] Real-time inference endpoint (<100ms)
- [ ] FastAPI backend with auth & monitoring
- [ ] Cosmos DB user profiles & baselines

### Phase 4: Frontend & Integration (Weeks 7-8)
- [ ] React dashboard with real-time alerts
- [ ] Graph visualizations & investigation tools
- [ ] SIEM integrations (Splunk, Sentinel)
- [ ] Docker & Kubernetes deployment

## 🧪 Testing

```bash
# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ --cov=. --cov-report=html

# Run specific test suite
pytest tests/unit/test_models.py -v

# Run integration tests
pytest tests/integration/ -v
```

## 📚 Documentation

- [Architecture Deep Dive](docs/ARCHITECTURE.md)
- [API Reference](docs/API_REFERENCE.md)
- [Deployment Guide](docs/DEPLOYMENT.md)
- [Model Documentation](docs/MODELS.md)
- [Contributing Guide](docs/CONTRIBUTING.md)

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](docs/CONTRIBUTING.md) for guidelines.

## 📜 License

MIT License - See LICENSE file for details

## 🏆 Imagine Cup 2026

This project is submitted to Microsoft Imagine Cup 2026 - Cybersecurity Category.

**Team**: NeuroShield Development Team  
**Organization**: IIT Madras  
**Contact**: dipayansardar73@gmail.com

---

**Built with ❤️ for enterprise security**
