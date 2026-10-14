# Mental-Health-Prediction-
The Mental Health Prediction System is a ML based project ,individuals monitor and understand their mental well-being based on their daily lifestyle activities, habits, and behavioral patterns. Machine Learning model analyzes the input and generates a Mental Health Score on a scale of 0 to 10
# 🧠 MENTAL HEALTH PREDICTOR

### AI-Powered Wellness Assessment & Lifestyle Insights

MENTAL HEALTH PREDICTOR is a machine learning-based web application that estimates a user's wellness score from everyday lifestyle patterns and provides general wellness recommendations.

The application combines a trained Extra Trees Regression model, a FastAPI backend, a React frontend, and an AI-powered chatbot to create an interactive assessment experience.

> **Disclaimer:** This is an educational project, not a clinically validated mental health assessment or diagnostic tool. Predictions and recommendations are not a substitute for professional care.

---

## ✨ Key Features

- 📊 **Wellness Score Prediction** — Estimates a score on a 0–10 scale using lifestyle-related inputs.
- 🧠 **Machine Learning Integration** — Uses an Extra Trees Regression model with a preprocessing pipeline.
- 😌 **Stress-Level Insight** — Applies a separate rule-based adjustment based on self-reported stress.
- 📈 **Assessment Analysis** — Displays the predicted score, its interpretation, and submitted lifestyle information.
- 💡 **Personalized Recommendations** — Offers general suggestions about sleep, screen time, physical activity, study habits, nutrition, hydration, mindfulness, and relaxation.
- 🤖 **AI Wellness Chatbot** — Provides conversational wellness guidance using assessment context.
- 📅 **Assessment History** — Stores recent assessments locally for later review.
- 👤 **User Interface** — Includes registration, login, profile, dashboard, settings, and support pages.
- 🆘 **Support Resources** — Provides support guidance and an emergency-calling link.
- 📱 **Responsive Dashboard** — Built with React and Tailwind CSS.

## 🛠️ Tech Stack

| Component           | Technologies                          |
| ------------------- | ------------------------------------- |
| Frontend            | React, Vite, Tailwind CSS, JavaScript |
| UI & Icons          | Lucide React                          |
| Backend             | Python, FastAPI, Uvicorn              |
| Machine Learning    | Scikit-learn, Extra Trees Regressor   |
| Data Processing     | Pandas, NumPy                         |
| Data Visualization  | Matplotlib, Seaborn, Jupyter Notebook |
| Model Serialization | Joblib / serialized model pipeline    |
| AI Chatbot          | Google Gemini API                     |
| Local Storage       | Browser LocalStorage                  |

## 🤖 Machine Learning Pipeline

The model was trained using lifestyle and digital-usage data.

### Input Features

- Age
- Gender
- Country
- Academic Level
- Most-Used Platform
- Purpose of Use
- Average Daily Usage Hours
- Daily Unlocks
- Study Hours
- Physical Activity Hours
- Sleep Hours per Night

**Note:** Stress level is handled separately and is not an input feature of the original trained Extra Trees model.

### Model Development

The machine learning workflow includes:

1. Data cleaning and duplicate removal.
2. Exploratory Data Analysis (EDA).
3. Numerical feature scaling.
4. Categorical feature encoding.
5. Train-test splitting.
6. Training and comparison of multiple regression models.
7. Cross-validation and model evaluation.
8. Saving the trained preprocessing and prediction pipeline.

The evaluated models included Linear Regression, Random Forest, Gradient Boosting, and Extra Trees Regression.

### 📊 Model Performance

The original Extra Trees model achieved the following results on the held-out test set:

| Metric                          | Result |
| ------------------------------- | -----: |
| Mean Absolute Error (MAE)       | 0.2236 |
| Root Mean Squared Error (RMSE)  | 0.3168 |
| R² Score                        | 0.9438 |
| Mean 5-Fold Cross-Validation R² | 0.9250 |

These results describe performance on the project's dataset. They do not establish clinical validity or guarantee accurate predictions for new users.

### Stress-Level Adjustment

The application applies a separate adjustment after the base model prediction.

| Self-Reported Stress Level | Adjustment |
| -------------------------- | ---------: |
| Low                        |      +0.30 |
| Medium                     |       0.00 |
| High                       |      −0.50 |

The adjusted score is bounded between 0 and 10.

> **Important:** These adjustments are application-defined values, not learned effects from the ML model or clinically validated weights. The displayed score combines the model prediction with a separate rule-based adjustment.

## 🏗️ Project Structure

```text
MENTAL_HEALTH/
│
├── backend/
│   ├── main.py
│   ├── routes/
│   │   └── prediction.py
│   ├── schemas/
│   │   ├── prediction.py
│   │   └── chat.py
│   ├── services/
│   │   └── chatbot.py
│   └── prediction/
│       └── predict.py
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── layouts/
│   │   ├── pages/
│   │   ├── context/
│   │   ├── services/
│   │   ├── app.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── package.json
│   └── vite.config.js
│
├── models/
│   ├── mental_health_pipeline.pkl
│   └── common_countries.pkl
│
├── data/
│   └── raw/
│       └── mini.csv
│
├── notebooks/
│   └── 01_eda.ipynb
│
├── .gitignore
└── README.md
```

This structure shows the main project components. Additional files may exist in the repository.

## ⚙️ Installation & Setup

### Prerequisites

Install the following before running the application:

- Python 3.10 or a compatible supported version
- Node.js and npm
- Git

### 1. Clone the Repository

Replace the placeholders with your actual GitHub repository details.

```bash
git clone https://github.com/gauravv-chauhan/Mental-Health-Prediction-.git
cd Mental-Health-Prediction-
```

### 2. Set Up the Python Backend

From the project root, create and activate a virtual environment.

**Windows PowerShell**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

Install the required backend packages:

```bash
pip install fastapi uvicorn pandas numpy scikit-learn joblib python-dotenv google-genai
```

If you have a `requirements.txt` containing your project's dependencies, install from that file instead.

### 3. Configure Environment Variables

If the chatbot uses the Gemini API, create a `.env` file inside the `backend/` directory.

```dotenv
GEMINI_API_KEY=your_gemini_api_key
```

Replace the placeholder with your own API key.

**Security reminders:**

- Never commit a real API key or other secrets to GitHub.
- Make sure `.env` is excluded in `.gitignore`.
- If a key was previously committed or pushed, revoke or rotate it. Removing it from the current file does not remove it from Git history.
- Keep your real `.env` file local. You can share a `.env.example` file containing placeholders instead.

### 4. Verify the Model Files

The backend expects these files, based on the current project setup:

```text
models/mental_health_pipeline.pkl
models/common_countries.pkl
```

Make sure they exist at the paths expected by your backend. If they are not included in the repository, regenerate them using the training notebook or your project's documented model setup process.

### 5. Start the Backend

Open a terminal and navigate to the backend directory:

```powershell
cd backend
uvicorn main:app --reload
```

The local API should be available at:

- **API:** `http://127.0.0.1:8000`
- **Interactive API documentation:** `http://127.0.0.1:8000/docs`

Keep the backend terminal running.

### 6. Start the Frontend

Open a second terminal at the project root:

```powershell
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, normally:

`http://localhost:5173`

Keep both terminals running while using the application.

## 🔄 Application Workflow

```text
User
  |
  v
React Assessment Form
  |
  v
FastAPI Prediction Endpoint
  |
  v
Saved ML Preprocessing Pipeline
  |
  v
Extra Trees Regression Model
  |
  v
Base Wellness Score
  |
  v
Separate Stress-Level Adjustment
  |
  v
Final Displayed Score
  |
  v
Score Interpretation, Recommendations & Chatbot
```

The AI chatbot is a separate feature that uses the configured Gemini API.

## 🔐 Privacy & Security

- Assessment history and demo account data may be stored in browser LocalStorage.
- LocalStorage is not secure authentication or encrypted health-data storage.
- Avoid entering sensitive personal information into a public demo.
- Keep API keys in environment variables and exclude `.env` from version control.
- The current local-storage-based account system is intended for demonstration, not production use.
- A production deployment should implement secure authentication, server-side authorization, data protection, and appropriate privacy controls.

## 🚧 Limitations

- The model was trained on a specific dataset and may not generalize to every population.
- Predictions reflect patterns learned from the dataset rather than a clinical assessment.
- Stress-level adjustments are rule-based and are not validated clinical measures.
- Recommendations are general wellness suggestions, not personalized medical treatment.
- Browser LocalStorage is not a secure production-grade account or health-data system.
- Performance on a held-out dataset does not guarantee performance on real-world users.

## 🔮 Future Improvements

- Interactive wellness “what-if” simulator.
- Explainable AI to show which features influenced a prediction.
- Wellness trends and longitudinal assessment charts.
- Weekly wellness summaries.
- Improved privacy and secure user authentication.
- More comprehensive model validation and bias analysis.
- Expanded support resources and accessibility improvements.

## 🎯 Project Objective

The goal of **MENTAL HEALTH PREDICTOR** is to demonstrate how machine learning, web development, and conversational AI can be combined into an interactive lifestyle-awareness application.

The project explores data-driven insights that encourage reflection on everyday habits while clearly distinguishing model predictions from professional mental health assessment.

## 👨‍💻 Author

**HARSH PATEL**
B.Tech Computer Science & Engineering Student

- GitHub: [gauravv-chauhan](https://github.com/gauravv-chauhan)
- LinkedIn: [Gaurav Singh](https://www.linkedin.com/in/gaurav-singh-3281a1381)

---









