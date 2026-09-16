````markdown
# 🏎️ GridPlay — F1 Telemetry, Prediction & Fan Battles

GridPlay is a full-stack Formula 1 analytics platform combining interactive race telemetry, machine learning-based post-qualifying predictions, and fan prediction battles.

## 🚀 Features

- 📡 **Telemetry Explorer** — Explore F1 race and driver telemetry with interactive D3.js visualizations.
- 🤖 **Race Prediction** — Generate predicted finishing probabilities from qualifying positions using a Logistic Regression model.
- ⚔️ **Fan vs AI Battles** — Submit race predictions, receive scores, and compete on race-specific leaderboards.
- 🔌 **REST API** — FastAPI backend for telemetry, prediction, and battle services.
- 💾 **Persistent Storage** — SQLite + SQLAlchemy for storing predictions and scores.
- 🐳 **Docker Support** — Containerized backend for deployment.
- 🧪 **Strategy Playground** — Interactive interface for experimenting with pit-stop laps and tyre compounds.

## 🧠 Machine Learning

The prediction system uses a pairwise classification approach.

For each pair of drivers, features are generated from their qualifying positions:

```text
[Driver A Qualifying Position,
 Driver B Qualifying Position,
 Position Difference]
````

A Logistic Regression model predicts the probability of one driver finishing ahead of another. Pairwise probabilities are then aggregated to produce driver-level finishing probabilities and a predicted order.

The trained model is serialized using Joblib.

## 📊 Telemetry

GridPlay integrates with **FastF1** to retrieve Formula 1 session and telemetry data.

The telemetry pipeline supports:

* Race selection
* Driver selection
* Lap data
* Lap times
* Sector times
* Speed
* Tyre compounds

When external telemetry data is unavailable, the application can fall back to bundled sample telemetry.

## 🏗️ Architecture

```text
React + D3.js Frontend
          │
          │ REST API
          ▼
     FastAPI Backend
     ┌────┼─────────┐
     ▼    ▼         ▼
 Telemetry Prediction Battles
     │       │         │
   FastF1   ML       SQLite
```

## 🛠️ Tech Stack

**Frontend:** React, Vite, JavaScript, Axios, D3.js, Tailwind CSS

**Backend:** Python, FastAPI, Pydantic, Uvicorn

**Machine Learning:** Scikit-learn, Logistic Regression, NumPy, Joblib

**Data & Storage:** FastF1, SQLite, SQLAlchemy, JSON

**Deployment:** Docker, Vercel

## 📁 Project Structure

```text
GridPlay/
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   │   ├── battles.py
│   │   │   ├── predict.py
│   │   │   └── telemetry.py
│   │   ├── models/
│   │   │   ├── predict_model.py
│   │   │   ├── train_pair_model.py
│   │   │   └── pair_model.joblib
│   │   ├── data/
│   │   ├── db.py
│   │   ├── models_db.py
│   │   └── main.py
│   ├── Dockerfile
│   └── requirements.txt
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── FanBattle.jsx
│   │   │   ├── PredictionKit.jsx
│   │   │   ├── StrategyPlayground.jsx
│   │   │   └── TelemetryExplorer.jsx
│   │   ├── api.js
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
│
└── package-lock.json
```

## 🔌 API

### Telemetry

```text
GET /api/telemetry/races
GET /api/telemetry/race/{race_id}/drivers
GET /api/telemetry/race/{race_id}/telemetry/{driver_id}
```

### Prediction

```text
POST /api/predict/post_qualifying
```

### Fan Battles

```text
POST /api/battles/submit
GET /api/battles/leaderboard/{race_id}
```

## 🚀 Run Locally

### Backend

```bash
git clone https://github.com/shnk7107/TeamAPEX_GridPlay_Code.git
cd TeamAPEX_GridPlay_Code/backend
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Backend:

```text
http://localhost:8000
```

API documentation:

```text
http://localhost:8000/docs
```

### Frontend

```bash
cd frontend
npm install
npm run dev
```

## 🐳 Docker

Build the backend:

```bash
docker build -t gridplay-backend ./backend
```

Run:

```bash
docker run -p 8000:8000 gridplay-backend
```

## 💡 Key Engineering Concepts

* Full-stack application development
* REST API design
* Frontend-backend integration
* Machine learning inference
* Pairwise classification
* Data visualization
* External API/data integration
* Database persistence
* Model serialization
* API validation
* Docker-based deployment
* Fault-tolerant data handling

## 🔮 Future Improvements

* Real race-result-based model training
* Additional ML models and features
* Weather and tyre strategy integration
* Realistic race-strategy simulation
* User authentication
* Real-time race data
* Production database support
* Automated model retraining
* Application monitoring

## 👨‍💻 Author

**Shashank Tadikamalla**
