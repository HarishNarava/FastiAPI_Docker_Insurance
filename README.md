# FastAPI Insurance Prediction

ML API that predicts insurance premium categories with confidence scores

## what it does
- predicts insurance premium (low/medium/high) using ML model
- validates user input automatically 
- calculates BMI, risk level, age groups, city tiers
- returns confidence scores and probability distributions
- has health check endpoint with model status

## run it
```bash
pip install -r requirements.txt
uvicorn app:app --reload
```

go to http://127.0.0.1:8000 to see it work

## endpoints  
- `/` - home message
- `/health` - check if model is loaded with version info
- `/predict` - get insurance prediction with confidence
- `/docs` - interactive api documentation

## example request
```bash
curl -X POST http://127.0.0.1:8000/predict \
  -H "Content-Type: application/json" \
  -d '{
    "age": 28,
    "weight": 70,
    "height": 1.75,
    "income_lpa": 5.5,
    "smoker": false,
    "city": "Mumbai", 
    "occupation": "private_job"
  }'
```

response:
```json
{
  "predicted_category": "Medium",
  "confidence": 0.8432,
  "class_probabilities": {
    "Low": 0.01,
    "Medium": 0.84,
    "High": 0.15
  }
}
```

## project structure
- `app.py` - main api with error handling
- `model/predict.py` - ml model and prediction logic
- `schema/user_input.py` - input validation
- `schema/prediction_response.py` - response structure
- `config/city_tiers.py` - city classifications
- `model.pkl` - trained random forest model

built with fastapi, scikit-learn, pydantic
