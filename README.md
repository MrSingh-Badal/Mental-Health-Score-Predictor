# 🧠 Mental Health Score Predictor

A full-stack machine learning web app that predicts a student's **mental health score (0–10)** from their daily habits — sleep, study time, screen time, physical activity, and stress level — using a model trained on real student social-media and lifestyle data.

Built as an end-to-end ML project: data exploration → model training → FastAPI backend → responsive vanilla JS frontend → live deployment.

> ⚠️ **Disclaimer:** This tool is for educational and self-reflection purposes only. It is **not** a clinical or diagnostic instrument. If you're struggling, please talk to a qualified mental health professional or someone you trust.

---

## ✨ Live Demo

🔗 **[Try it here](https://mental-health-score-predictor-1-x2ou.onrender.com)**

> Hosted on Render's free tier — the backend may take 30–60s to spin up on first request if it's been idle.

---

## 📸 Overview

The app asks for a few quick details about a student's day-to-day habits and returns a predicted wellness score, visualized on a gauge, along with general, non-clinical wellness suggestions.

| Section | What it does |
|---|---|
| **Profile** | Age, gender, country |
| **Academic & Digital Habits** | Academic level, most-used platform, purpose of use, daily screen time, phone unlocks |
| **Lifestyle & Stress** | Study hours, physical activity, sleep, perceived stress level |
| **Result** | Predicted score (0–10) with a visual gauge and contextual read |

---

## 🏗️ Tech Stack

**Backend**
- [FastAPI](https://fastapi.tiangolo.com/) — REST API serving the model
- [Pydantic](https://docs.pydantic.dev/) — request/response schema validation
- [scikit-learn](https://scikit-learn.org/) — trained prediction pipeline (`ColumnTransformer` + regressor)
- [pandas](https://pandas.pydata.org/) / [joblib](https://joblib.readthedocs.io/) — data handling and model serialization
- [Uvicorn](https://www.uvicorn.org/) — ASGI server

**Frontend**
- Vanilla **HTML5 / CSS3 / JavaScript** — no frameworks
- Communicates with the backend via `fetch()` against the `/predict` REST endpoint

**Model Development**
- `mental_health.ipynb` — data cleaning, EDA, feature engineering, and model training on the dataset below

**Deployment**
- [Render](https://render.com/) — backend (and static frontend) hosting

---

## 📊 Dataset

`Student Social Media And Mental Health Impact.csv`

Contains per-student records of demographics, academic level, social media usage patterns, and lifestyle habits (sleep, study, physical activity, stress) used to train a regression model that predicts an overall mental health score.

---

## 🔌 API Reference

### `GET /`
Health check.
```json
{ "Welcome Guys" }
```

### `POST /predict`
Runs the model on a student's habit data and returns a predicted score.

**Request body**

```json
{
  "age": 21,
  "gender": "Male",
  "country": "India",
  "academic_level": "Undergraduate",
  "most_used_platform": "Instagram",
  "purpose_of_use": "Entertainment",
  "avg_daily_usage_hours": 4.5,
  "daily_unlocks": 60,
  "study_hours": 3.0,
  "physical_activity_hours": 1.0,
  "sleep_hours_per_night": 6.5,
  "stress_level": "Medium"
}
```

| Field | Type | Constraints |
|---|---|---|
| `age` | int | 10–100 |
| `gender` | string | `Male`, `Female` |
| `country` | string | free text |
| `academic_level` | string | `High School`, `Undergraduate`, `Graduate` |
| `most_used_platform` | string | `Facebook`, `LinkedIn`, `Instagram`, `Snapchat`, `Twitter`, `YouTube`, `TikTok`, `LINE`, `KakaoTalk`, `VKontakte`, `WhatsApp`, `WeChat` |
| `purpose_of_use` | string | `Networking`, `Education`, `Entertainment`, `News` |
| `avg_daily_usage_hours` | float | 0–24 |
| `daily_unlocks` | int | ≥ 0 |
| `study_hours` | float | 0–24 |
| `physical_activity_hours` | float | 0–24 |
| `sleep_hours_per_night` | float | 0–24 |
| `stress_level` | string | `Low`, `Medium`, `High`, `Very High` |

**Response**

```json
{ "predicted_mental_health_score": 6.77 }
```

Interactive Swagger docs are available at **`/docs`** once the server is running.

---

## 🚀 Running Locally

### 1. Clone the repo
```bash
git clone https://github.com/MrSingh-Badal/Mental-Health-Score-Predictor.git
cd Mental-Health-Score-Predictor
```

### 2. Set up a virtual environment (recommended)
```bash
python -m venv venv
# Windows
venv\Scripts\activate
# macOS/Linux
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the backend
```bash
uvicorn main:app --reload
```
The API will be live at `http://127.0.0.1:8000`, with docs at `http://127.0.0.1:8000/docs`.

### 5. Run the frontend
Open `index.html` directly in a browser, or serve it locally:
```bash
python -m http.server 5500
```
Then visit `http://localhost:5500/index.html`.

> **Note:** `script.js` has an `API_BASE`/`API_BASE_URL` constant at the top — point it at `http://127.0.0.1:8000` for local development, or your deployed backend URL for production.

---

## ☁️ Deployment (Render)

**Build command**
```bash
pip install -r requirements.txt
```

**Start command**
```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

> ⚠️ Render runs on Linux, which is **case-sensitive** for filenames — unlike Windows. Make sure the filename referenced in `main.py` (`joblib.load(...)`) exactly matches the case of the `.pkl` file in the repo.

---

## 📁 Project Structure

```
Mental-Health-Score-Predictor/
├── main.py                                            # FastAPI backend & prediction endpoint
├── mental_health.ipynb                                # EDA + model training notebook
├── Mental_Health_Model.pkl                             # Trained sklearn pipeline
├── Student Social Media And Mental Health Impact.csv   # Training dataset
├── requirements.txt                                    # Python dependencies
├── index.html                                          # Frontend markup
├── style.css                                           # Frontend styling
├── script.js                                           # Frontend logic & API integration
└── README.md
```

---

## 🗺️ Roadmap / Ideas

- [ ] Separate frontend and backend into distinct deployable services
- [ ] Add model explainability (e.g. SHAP values) to show which habits most influenced a score
- [ ] Add authentication + history if turned into a multi-user tool
- [ ] Expand dataset/model to reduce bias across countries and demographics

---

## 🤝 Contributing

Issues and pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is open source. Add a license of your choice (e.g. MIT) via a `LICENSE` file if you plan to share or accept contributions.

---

## 👤 Author

**Badal Singh**
Final-year B.Tech, Electronics and Communication Engineering, BIT Mesra
GitHub: [@MrSingh-Badal](https://github.com/MrSingh-Badal)
