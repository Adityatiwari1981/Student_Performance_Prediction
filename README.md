# Student Performance Prediction System

A Machine Learning-based web application that predicts student academic performance using various academic, behavioral, and environmental factors. This system helps educators and institutions identify at-risk students early and take proactive measures to improve outcomes.

---

## 📋 Project Objectives

The Student Performance Prediction System is designed to:

- **Predict Student Performance**: Classify students into performance categories (Poor, Average, Excellent) based on multiple factors
- **Early Intervention**: Identify at-risk students early to enable timely support and intervention
- **Data-Driven Insights**: Provide educators with actionable insights based on comprehensive analysis of student factors
- **Institutional Support**: Help educational institutions optimize resource allocation and support programs
- **Multi-Factor Analysis**: Consider academic, behavioral, environmental, and personal factors in predictions

---

## 🏗️ Architecture Overview

The system follows a **Client-Server Architecture** with a Machine Learning backbone:

```
┌─────────────────────────────────────────────────────────────┐
│                    Frontend (Web UI)                         │
│          HTML / CSS / JavaScript Interface                   │
│          - Form Input Collection                             │
│          - Result Display & Visualization                    │
└────────────────────┬────────────────────────────────────────┘
                     │ HTTP Requests/Responses
                     │
┌────────────────────▼────────────────────────────────────────┐
│                  Flask Backend Server                        │
│                 (REST API Layer)                             │
│    ├─ Home Route (/)                                         │
│    ├─ Prediction API (/predict)                              │
│    ├─ Test Route (/test)                                     │
│    └─ Favicon Route (/favicon.ico)                           │
└────────────────────┬────────────────────────────────────────┘
                     │ Data Processing & Feature Engineering
                     │
┌────────────────────▼────────────────────────────────────────┐
│            Machine Learning Model Engine                     │
│                (trained model - .pkl)                        │
│       ├─ Feature Engineering                                 │
│       ├─ One-Hot Encoding                                    │
│       ├─ Model Inference                                     │
│       └─ Probability Calculation                             │
└─────────────────────────────────────────────────────────────┘
```

### Key Components:

1. **Frontend**: Interactive web interface built with HTML, CSS, and JavaScript
2. **Backend API**: Flask-based REST API server handling HTTP requests
3. **ML Model**: Pre-trained scikit-learn model (`students.pkl`)
4. **Data Processing**: Feature engineering pipeline for input transformation

---

## 📁 Project Structure

```
Student_Performance_Prediction/
│
├── README.md                          # Project documentation
├── LICENSE                            # License file
├── TODO.md                            # Task tracking
├── Student_performance.csv            # Raw training data
│
├── Notebooks/
│   ├── Student_per.ipynb             # Initial EDA and model exploration
│   ├── Student_per_final.ipynb       # Final model training
│   └── Lovepreet_performance.ipynb   # Additional analysis
│
├── backend/                           # Flask application
│   ├── app.py                        # Main Flask application
│   ├── config.py                     # Configuration settings
│   ├── requirements.txt              # Python dependencies
│   │
│   ├── ml_model/
│   │   └── students.pkl              # Trained ML model
│   │
│   ├── static/                       # Static assets
│   │   ├── style.css                 # Frontend styling
│   │   ├── script.js                 # Frontend JavaScript
│   │   └── images/
│   │       └── ha.jfif               # Application images
│   │
│   └── templates/
│       └── index.html                # HTML template
│
└── previous_model/                   # Archived/previous models
```

---

## Input Features

The model accepts the following student attributes:

### Academic Factors
- **Study Hours**: Daily hours spent on studying (numeric)
- **Class Attendance**: Attendance percentage (0-100)
- **Course**: Degree program (B.Com, B.Sc, B.Tech, BA, BBA, BCA, Diploma)
- **Exam Difficulty**: Perceived exam difficulty level (1-5 scale)

### Behavioral Factors
- **Study Method**: Learning approach (Self-study, Group study, Coaching, Online videos, Mixed)
- **Grade**: Current academic grade/performance level

### Environmental Factors
- **Internet Access**: Availability of internet (Yes/No)
- **Facility Rating**: Access to study facilities (1-5 scale)

### Personal Factors
- **Age**: Student age (numeric)
- **Gender**: Gender identity (Male, Female, Other)
- **Sleep Hours**: Daily sleep duration (numeric)
- **Sleep Quality**: Quality of sleep (1-5 scale)

---

## 🚀 Quick Start Guide

### Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Git

### Installation & Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/AshishRastogi123/Student_Performance_Prediction
   cd Student_Performance_Prediction
   ```

2. **Create Virtual Environment**
   ```bash
   cd backend
   python -m venv venv
   ```

3. **Activate Virtual Environment**
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```
   - On macOS/Linux:
     ```bash
     source venv/bin/activate
     ```

4. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

5. **Verify Model is Present**
   - Ensure `ml_model/students.pkl` exists in the backend directory

6. **Run the Application**
   ```bash
   python app.py
   ```

7. **Access the Application**
   - Open your browser and navigate to: `http://localhost:5000`

---

## 🔌 API Endpoints

### 1. Home Page
- **Endpoint**: `GET /`
- **Description**: Serves the main web interface
- **Response**: HTML interface

### 2. Prediction API
- **Endpoint**: `POST /predict`
- **Description**: Predicts student performance based on provided attributes
- **Request Type**: Form Data
- **Request Parameters**:
  ```
  age (numeric)
  gender (string: male, female, other)
  study_hours (numeric)
  attendance (0-100)
  internet (0 or 1)
  sleep_hours (numeric)
  sleep_quality (1-5)
  facility (1-5)
  exam_diff (1-5)
  course (string: b.com, b.sc, b.tech, ba, bba, bca, diploma)
  method (string: self-study, group study, coaching, online videos, mixed)
  ```

- **Response** (Success):
  ```json
  {
    "success": true,
    "prediction": "Excellent",
    "confidence": 95.23,
    "label": 2,
    "probs": [0.02, 0.03, 0.95]
  }
  ```

- **Response** (Error):
  ```json
  {
    "success": false,
    "error": "Missing fields: [...]"
  }
  ```

### 3. Test Route
- **Endpoint**: `GET /test`
- **Description**: Health check endpoint to verify server is running
- **Response**: 
  ```json
  {
    "status": "SERVER WORKING",
    "message": "All good!"
  }
  ```

### 4. Favicon
- **Endpoint**: `GET /favicon.ico`
- **Description**: Returns 404 as favicon is not available
- **Response**: Empty with 404 status

---

## 🤖 Machine Learning Model

### Model Type
- **Algorithm**: Scikit-learn based classification model
- **Output Classes**: 
  - 0: Poor Performance
  - 1: Average Performance
  - 2: Excellent Performance

### Model Pipeline
1. **Feature Input**: Receives 25+ features after one-hot encoding
2. **Feature Engineering**:
   - Gender one-hot encoding (3 features)
   - Course one-hot encoding (7 features)
   - Study method one-hot encoding (5 features)
3. **Prediction**: Returns class label and probability distribution
4. **Confidence Score**: Calculated from maximum probability

### Model Features
- **Total Features**: 25+ features after encoding
- **Prediction Type**: Multi-class classification
- **Confidence Metrics**: Probability scores for each class

---

## 📊 Technologies Used

### Frontend
- **HTML5**: Structure
- **CSS3**: Styling
- **JavaScript (Vanilla)**: Client-side logic and interactivity

### Backend
- **Flask**: Lightweight web framework
- **Python 3.8+**: Main programming language

### Machine Learning
- **scikit-learn**: Model training and inference
- **joblib**: Model serialization/deserialization
- **pandas**: Data manipulation and processing
- **numpy**: Numerical computations

### Data Processing
- **CSV**: Data storage format
- **Jupyter Notebooks**: Model development and analysis

---

## 📈 Usage Example

### Via Web Interface
1. Open `http://localhost:5000` in browser
2. Fill in the student information form
3. Submit the form
4. View the prediction result with confidence score

### Via API (cURL)
```bash
curl -X POST http://localhost:5000/predict \
  -d "age=20&gender=male&study_hours=5&attendance=85&internet=1&sleep_hours=7&sleep_quality=4&facility=4&exam_diff=3&course=b.tech&method=mixed"
```

---

## 🔍 Debugging & Logging

The application includes comprehensive logging:
- **Request Logging**: All HTTP requests are logged with method and path
- **Feature Logging**: Input data transformation steps are logged
- **Model Logging**: Model loading and prediction details are logged
- **Error Logging**: Full traceback for debugging purposes

Check console output for detailed debug information during requests.

---

## 📝 Model Training

For information about model training and data preparation:
- See `Student_per_final.ipynb` for final model training pipeline
- See `Student_per.ipynb` for initial exploration
- See `Lovepreet_performance.ipynb` for additional analysis

---

## 📄 License

This project is licensed under the terms specified in the LICENSE file.

---

## 🤝 Contributing

Contributions are welcome! Please ensure:
- Code follows Python best practices
- Changes are tested thoroughly
- Documentation is updated accordingly

---

## 📞 Support & Issues

For issues or questions:
1. Check the TODO.md file for known issues
2. Review the error logs in console output
3. Ensure all dependencies are properly installed
4. Verify the model file exists at `backend/ml_model/students.pkl`

---

## 🎯 Future Enhancements

Potential improvements for future versions:
- Database integration for student data persistence
- Multi-model ensemble predictions
- Real-time performance tracking dashboard
- Export prediction reports (PDF/Excel)
- Authentication and user management
- Batch prediction capability
- Model retraining pipeline
- Advanced analytics and visualization

---

**Last Updated**: April 2026
