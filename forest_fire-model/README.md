# Forest Fire — Fire Weather Index (FWI) Predictor

A Flask web app that predicts the **Fire Weather Index (FWI)** from weather and fuel-moisture readings, using a Ridge Regression model trained on the UCI Algerian Forest Fires dataset (Bejaia and Sidi-Bel Abbès regions).

Enter temperature, humidity, wind speed, rainfall, and the FFMC / DMC / ISI fuel codes, and the app returns a predicted FWI value indicating fire danger.

---

## Project structure

```
forest_fire-model/
├── application.py          # Flask app entry point
├── models/
│   ├── ridge.pkl            # Trained Ridge Regression model
│   └── scaler.pkl            # Fitted StandardScaler used to preprocess inputs
├── templates/
│   ├── index.html             # Landing page
│   └── home.html              # Prediction form + result display
└── requirements.txt
```

## How it works

1. **Enter conditions** — Temperature, Relative Humidity, Wind Speed, Rain, FFMC, DMC, ISI, Classes, and Region on the form.
2. **Scale & predict** — Inputs are transformed with the saved `scaler.pkl`, then passed to `ridge.pkl` for prediction.
3. **Read the index** — The predicted FWI is rendered back on the page. Higher values indicate greater fire danger.

## Input fields

| Field | Description | Typical range |
|---|---|---|
| Temperature | Air temperature (°C) | 22–42 |
| RH | Relative Humidity (%) | 21–90 |
| Ws | Wind Speed (km/h) | 6–29 |
| Rain | Total rainfall (mm) | 0–16.8 |
| FFMC | Fine Fuel Moisture Code | 28–92 |
| DMC | Duff Moisture Code | 1–65 |
| ISI | Initial Spread Index | 0–19 |
| Classes | Observed fire occurrence (Fire = 1, Not Fire = 0) | 0 or 1 |
| Region | Weather station (Bejaia = 0, Sidi-Bel Abbès = 1) | 0 or 1 |

## Setup

**1. Clone the repository**
```bash
git clone <your-repo-url>
cd forest_fire-model
```

**2. Create a virtual environment**
```bash
python -m venv venv
venv\Scripts\activate      # Windows
source venv/bin/activate    # macOS/Linux
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Run the app**
```bash
python application.py
```

The app runs at `http://0.0.0.0:5000` (or `http://localhost:5000`) by default.

## requirements.txt

```
Flask
numpy
pandas
scikit-learn
```

## Routes

| Route | Method | Description |
|---|---|---|
| `/` | GET | Landing page |
| `/predictdata` | GET | Displays the prediction form |
| `/predictdata` | POST | Accepts form inputs, returns predicted FWI |

## Notes

- Predictions are only as reliable as the training data — the model was trained on data from two specific weather stations in Algeria, so results outside that region or those seasonal conditions should be treated as indicative rather than authoritative.
- Not a substitute for official fire-danger advisories.

## Tech stack

- **Backend:** Flask
- **Model:** scikit-learn Ridge Regression + StandardScaler
- **Frontend:** HTML/CSS (Jinja2 templating)