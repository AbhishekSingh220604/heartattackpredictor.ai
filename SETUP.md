# Quick Setup Guide: Connecting to Your Render API

## Step 1: Find Your Render API URL

1. Go to your Render dashboard: https://dashboard.render.com/
2. Click on your heart attack prediction service
3. Copy your service URL (it looks like: `https://your-app-name.onrender.com`)
4. Add `/predict` to the end (or whatever your prediction endpoint is)

Example: `https://heart-attack-model-xyz.onrender.com/predict`

## Step 2: Update index.html

Open `index.html` and go to line 592. Replace:

```javascript
const API_ENDPOINT = 'https://your-render-app.onrender.com/predict';
```

With your actual URL:

```javascript
const API_ENDPOINT = 'https://heart-attack-model-xyz.onrender.com/predict';
```

## Step 3: Enable CORS in Your Render App

Your backend MUST allow requests from your GitHub Pages domain. Add this to your Python code:

### If using Flask:

```python
from flask import Flask, request, jsonify
from flask_cors import CORS
import numpy as np

app = Flask(__name__)
CORS(app)  # This allows all origins

@app.route('/predict', methods=['POST'])
def predict():
    try:
        data = request.get_json()
        
        # Extract features in the correct order
        features = [
            data['age'],
            data['sex'],
            data['cp'],
            data['trestbps'],
            data['chol'],
            data['fbs'],
            data['restecg'],
            data['thalach'],
            data['exang'],
            data['oldpeak'],
            data['slope'],
            data['ca'],
            data['thal']
        ]
        
        # Make prediction using your model
        prediction = model.predict([features])[0]
        probability = model.predict_proba([features])[0][1] * 100
        
        return jsonify({
            'prediction': int(prediction),
            'probability': float(probability)
        })
    
    except Exception as e:
        return jsonify({'error': str(e)}), 400

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

### If using FastAPI:

```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware
from pydantic import BaseModel
import numpy as np

app = FastAPI()

# Enable CORS
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Allows all origins
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

class PredictionInput(BaseModel):
    age: int
    sex: int
    cp: int
    trestbps: int
    chol: int
    fbs: int
    restecg: int
    thalach: int
    exang: int
    oldpeak: float
    slope: int
    ca: int
    thal: int

@app.post("/predict")
def predict(input_data: PredictionInput):
    try:
        features = [
            input_data.age,
            input_data.sex,
            input_data.cp,
            input_data.trestbps,
            input_data.chol,
            input_data.fbs,
            input_data.restecg,
            input_data.thalach,
            input_data.exang,
            input_data.oldpeak,
            input_data.slope,
            input_data.ca,
            input_data.thal
        ]
        
        # Make prediction
        prediction = model.predict([features])[0]
        probability = model.predict_proba([features])[0][1] * 100
        
        return {
            'prediction': int(prediction),
            'probability': float(probability)
        }
    
    except Exception as e:
        return {'error': str(e)}
```

## Step 4: Install Required Package

Add this to your `requirements.txt` on Render:

```
flask-cors
```

or for FastAPI:

```
fastapi
uvicorn
```

## Step 5: Deploy to GitHub Pages

```bash
git add .
git commit -m "Add heart attack prediction website"
git push origin main
```

Then enable GitHub Pages in your repository settings.

## Step 6: Test Your Setup

1. Open your GitHub Pages URL
2. Fill in the form with test data
3. Click "Analyze Risk"
4. Check browser console (F12) for any errors

### Common Issues:

**❌ CORS Error**: Add CORS headers to your Render backend
**❌ 404 Error**: Check your API endpoint URL
**❌ 500 Error**: Check your backend logs on Render
**❌ Network Error**: Make sure your Render service is running

## Testing Example

Test with these values:
- Age: 45
- Sex: Male (1)
- Chest Pain: Atypical Angina (1)
- Rest BP: 130
- Cholesterol: 250
- Fasting BS: No (0)
- Rest ECG: Normal (0)
- Max HR: 150
- Exercise Angina: No (0)
- Oldpeak: 2.5
- Slope: Flat (1)
- Vessels: 0
- Thal: Reversible Defect (2)

## Need Help?

1. Check Render logs for backend errors
2. Check browser console (F12) for frontend errors
3. Test your API directly with Postman
4. Make sure your model is loaded correctly in the backend

---

🎉 Once everything is connected, your site will be live and functional!
