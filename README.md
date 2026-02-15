# CardioPredict - Heart Attack Prediction Model

A modern, AI-powered web interface for heart attack risk assessment using machine learning.

![CardioPredict Preview](preview.png)

## 🚀 Live Demo

Visit: [Your GitHub Pages URL]

## ✨ Features

- **Modern UI/UX**: Sleek, medical-tech inspired design with smooth animations
- **Real-time Predictions**: Instant risk assessment using your deployed ML model
- **Responsive Design**: Works perfectly on desktop, tablet, and mobile devices
- **13 Medical Parameters**: Comprehensive cardiovascular health analysis
- **Visual Risk Indicator**: Clear, color-coded risk assessment display

## 🛠️ Setup Instructions

### 1. Configure Your Render API Endpoint

Open `index.html` and find line 592:

```javascript
const API_ENDPOINT = 'https://your-render-app.onrender.com/predict';
```

Replace with your actual Render API URL:

```javascript
const API_ENDPOINT = 'https://your-actual-app-name.onrender.com/predict';
```

### 2. Deploy to GitHub Pages

#### Option A: Using GitHub Web Interface

1. Create a new repository on GitHub (or use existing one)
2. Upload `index.html` to the repository
3. Go to **Settings** → **Pages**
4. Under **Source**, select **Deploy from a branch**
5. Choose **main** branch and **/ (root)** folder
6. Click **Save**
7. Your site will be live at `https://yourusername.github.io/repository-name/`

#### Option B: Using Git Command Line

```bash
# Initialize git repository (if not already done)
git init

# Add your files
git add index.html README.md

# Commit your changes
git commit -m "Initial commit: Heart attack prediction website"

# Add your GitHub repository as remote
git remote add origin https://github.com/yourusername/your-repo-name.git

# Push to GitHub
git push -u origin main

# Enable GitHub Pages in repository settings
```

### 3. Configure CORS on Your Render Backend

Your Render API needs to allow cross-origin requests from your GitHub Pages site. Add CORS headers to your backend:

**For Flask:**
```python
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)  # Enable CORS for all routes

@app.route('/predict', methods=['POST'])
def predict():
    # Your prediction logic here
    pass
```

**For FastAPI:**
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # In production, specify your GitHub Pages URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post("/predict")
def predict():
    # Your prediction logic here
    pass
```

## 📊 API Request Format

The frontend sends a POST request with the following JSON structure:

```json
{
  "age": 45,
  "sex": 1,
  "cp": 2,
  "trestbps": 120,
  "chol": 200,
  "fbs": 0,
  "restecg": 0,
  "thalach": 150,
  "exang": 0,
  "oldpeak": 2.5,
  "slope": 1,
  "ca": 0,
  "thal": 1
}
```

### Expected API Response Format

Your Render API should return JSON in one of these formats:

**Option 1:**
```json
{
  "prediction": 1,
  "probability": 75.5
}
```

**Option 2:**
```json
{
  "result": 1,
  "confidence": 0.755
}
```

The frontend will handle both formats automatically.

## 🎨 Customization

### Changing Colors

Edit the CSS variables in `index.html` (lines 10-17):

```css
:root {
    --primary: #ff1744;        /* Main red color */
    --secondary: #00e5ff;      /* Accent cyan color */
    --bg-dark: #0a0e27;        /* Background */
    --bg-card: #141932;        /* Card background */
    --text: #e0e6ed;           /* Main text color */
    --text-dim: #8892a6;       /* Secondary text */
}
```

### Changing Title and Branding

1. Update the `<title>` tag (line 7)
2. Update the `<h1>` tag (line 294)
3. Update the subtitle (line 305)
4. Update footer text (lines 391-393)

## 📱 Features Included

- ✅ Animated grid background
- ✅ Floating gradient orbs
- ✅ Smooth form animations
- ✅ Real-time API integration
- ✅ Loading states and error handling
- ✅ Responsive mobile design
- ✅ Risk visualization with color coding
- ✅ Animated heartbeat ECG line
- ✅ Information cards
- ✅ Professional typography

## 🔧 Troubleshooting

### API Connection Issues

1. **Check CORS**: Make sure your Render backend has CORS enabled
2. **Verify URL**: Confirm your API_ENDPOINT is correct
3. **Check Console**: Open browser DevTools (F12) and check the Console tab for errors
4. **Test API**: Use Postman or curl to test your Render endpoint directly

### GitHub Pages Not Updating

1. Wait 2-3 minutes after pushing changes
2. Hard refresh your browser (Ctrl+Shift+R or Cmd+Shift+R)
3. Clear browser cache
4. Check GitHub Actions tab for deployment status

## 📝 Model Parameters Explained

| Parameter | Description | Values |
|-----------|-------------|--------|
| **age** | Age in years | 1-120 |
| **sex** | Gender | 1 (Male), 0 (Female) |
| **cp** | Chest pain type | 0-3 |
| **trestbps** | Resting blood pressure (mm Hg) | 50-300 |
| **chol** | Serum cholesterol (mg/dl) | 100-600 |
| **fbs** | Fasting blood sugar > 120 mg/dl | 1 (Yes), 0 (No) |
| **restecg** | Resting ECG results | 0-2 |
| **thalach** | Maximum heart rate achieved | 60-220 |
| **exang** | Exercise induced angina | 1 (Yes), 0 (No) |
| **oldpeak** | ST depression induced by exercise | 0-10 |
| **slope** | Slope of peak exercise ST segment | 0-2 |
| **ca** | Number of major vessels | 0-4 |
| **thal** | Thalassemia | 0-2 |

## 🤝 Contributing

Feel free to fork this repository and make improvements! Some ideas:

- Add data visualization charts
- Implement patient history tracking
- Add export/download functionality
- Create a comparison tool
- Add more detailed risk breakdowns

## ⚠️ Disclaimer

This tool is for **educational and research purposes only**. It should not be used as a substitute for professional medical advice, diagnosis, or treatment. Always consult qualified healthcare professionals for medical concerns.

## 📄 License

MIT License - feel free to use this project for your portfolio or research.

## 🙏 Acknowledgments

- Machine learning model deployed on Render
- Design inspired by modern medical technology interfaces
- Fonts: Unbounded and JetBrains Mono from Google Fonts

---

Made with ❤️ for better healthcare through AI
