# 🔐 Network Security — Phishing Detection System

A machine learning-based end-to-end phishing URL detection system with a FastAPI serving layer, MLflow experiment tracking, MongoDB data storage, and a CI/CD pipeline via GitHub Actions.

---

## 📌 Overview

This project builds a complete MLOps pipeline to classify network traffic/URLs as phishing or legitimate. It covers data ingestion from MongoDB, feature engineering, model training with experiment tracking, and a REST API for real-time predictions.

---

## 🏗️ Project Structure

```
Network_Security/
├── networksecurity/          # Core Python package
│   ├── constants/            # Pipeline constants (DB names, paths, etc.)
│   ├── exception/            # Custom exception handling
│   ├── logging/              # Logging configuration
│   ├── pipeline/             # Training and prediction pipelines
│   └── utils/                # ML utilities, model estimator, helpers
├── Data_Schema/              # Data schema definitions
├── Network_Data/             # Raw network/phishing datasets
├── final_model/              # Saved preprocessor and trained model
├── prediction_output/        # CSV outputs from prediction endpoint
├── valid_data/               # Validated data artifacts
├── templates/                # Jinja2 HTML templates (prediction table)
├── .github/workflows/        # CI/CD GitHub Actions configuration
├── app.py                    # FastAPI application entry point
├── main.py                   # Training pipeline runner
├── push_data.py              # Script to push data to MongoDB
├── Dockerfile                # Container build configuration
├── requirements.txt          # Python dependencies
└── setup.py                  # Package setup
```

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3.x |
| API Framework | FastAPI + Uvicorn |
| ML | Scikit-learn |
| Experiment Tracking | MLflow + DagsHub |
| Data Storage | MongoDB Atlas |
| Containerization | Docker |
| CI/CD | GitHub Actions |
| Data Processing | Pandas, NumPy |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- MongoDB Atlas account
- Docker (optional)

### 1. Clone the Repository

```bash
git clone https://github.com/nihal00753/Network_Security.git
cd Network_Security
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Up Environment Variables

Create a `.env` file in the project root:

```env
MONGODB_URL_KEY=your_mongodb_connection_string
```

### 4. Push Data to MongoDB

```bash
python push_data.py
```

### 5. Run the Training Pipeline

```bash
python main.py
```

This will execute data ingestion, validation, transformation, model training, and evaluation stages sequentially.

---

## 🌐 API Usage

### Start the Server

```bash
python app.py
```

The API will be available at `http://localhost:8000`. Visit `/docs` for the interactive Swagger UI.

### Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/` | Redirects to Swagger docs |
| GET | `/train` | Triggers the full training pipeline |
| POST | `/predict` | Upload a CSV file and get predictions |

### Example Prediction Request

```bash
curl -X POST "http://localhost:8000/predict" \
  -F "file=@your_data.csv"
```

The response is an HTML table with predictions appended as a `predicted_column`. Results are also saved to `prediction_output/output.csv`.

---

## 🐳 Docker

### Build the Image

```bash
docker build -t network-security .
```

### Run the Container

```bash
docker run -p 8000:8000 --env-file .env network-security
```

---

## 📊 Experiment Tracking

This project uses **MLflow** with **DagsHub** for tracking experiments, metrics, and model artifacts. After training, open the MLflow UI:

```bash
mlflow ui
```

Or view experiments on your DagsHub repository dashboard.

---

## 🔄 CI/CD Pipeline

The `.github/workflows/` directory contains GitHub Actions workflows that automate testing and deployment on every push to `main`.

---

## 📦 Dependencies

Key packages from `requirements.txt`:

- `fastapi`, `uvicorn`, `python-multipart` — API server
- `scikit-learn` — ML model training
- `mlflow`, `dagshub` — experiment tracking
- `pymongo`, `certifi` — MongoDB connection
- `pandas`, `numpy` — data processing
- `python-dotenv` — environment variable management
- `pyyaml` — configuration files

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is open source. See the repository for details.
