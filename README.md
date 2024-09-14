# Profile Recommendation System

This Flask application provides a simple profile recommendation system using a K-Nearest Neighbors (KNN) algorithm. The system matches profiles based on their country and followed topics.

## Model Type

- **Model**: K-Nearest Neighbors (KNN)
- **Learning Type**: Unsupervised Learning
- **Metric**: Cosine Similarity
- **Features**:
  - Country (One-hot encoded)
  - Topics (MultiLabel Binarization)

## API Endpoints

### 1. Train the Model

**Endpoint**: `/train`  
**Method**: POST  
**Content-Type**: `application/json`

**Request Body**:
```json
{
  "current_profile": {
    "country": "Australia",
    "topics": ["Technology", "Economics"]
  },
  "other_profiles": [
    {
      "country": "Australia",
      "topics": ["Technology", "Sports"]
    },
    {
      "country": "Canada",
      "topics": ["Economics", "Politics"]
    },
    {
      "country": "UK",
      "topics": ["Technology", "Economics"]
    },
    {
      "country": "France",
      "topics": ["Sports", "Economics"]
    },
    {
      "country": "India",
      "topics": ["Technology", "Education"]
    }
  ]
}


Description: Trains the recommendation model using the provided profiles and saves it as a .pkl file.Response:{
  "message": "Model trained and saved successfully!"
}Example curl Command:curl -X POST http://localhost:5000/train \
-H "Content-Type: application/json" \
-d '{
  "current_profile": {
    "country": "Australia",
    "topics": ["Technology", "Economics"]
  },
  "other_profiles": [
    {
      "country": "Australia",
      "topics": ["Technology", "Sports"]
    },
    {
      "country": "Canada",
      "topics": ["Economics", "Politics"]
    },
    {
      "country": "UK",
      "topics": ["Technology", "Economics"]
    },
    {
      "country": "France",
      "topics": ["Sports", "Economics"]
    },
    {
      "country": "India",
      "topics": ["Technology", "Education"]
    }
  ]
}'2. Get RecommendationsEndpoint: /recommend
Method: POST
Content-Type: application/jsonRequest Body:{
  "current_profile": {
    "country": "Australia",
    "topics": ["Technology", "Economics"]
  }
}Description: Retrieves recommendations based on the current profile using the trained model.Response:{
  "recommendations": [
    {
      "profile": {
        "country": "Australia",
        "topics": ["Technology", "Sports"]
      },
      "similarity_score": 0.6666666666666669
    },
    {
      "profile": {
        "country": "UK",
        "topics": ["Technology", "Economics"]
      },
      "similarity_score": 0.6666666666666669
    },
    {
      "profile": {
        "country": "Canada",
        "topics": ["Economics", "Politics"]
      },
      "similarity_score": 0.3333333333333335
    },
    {
      "profile": {
        "country": "France",
        "topics": ["Sports", "Economics"]
      },
      "similarity_score": 0.3333333333333335
    },
    {
      "profile": {
        "country": "India",
        "topics": ["Technology", "Education"]
      },
      "similarity_score": 0.3333333333333335
    }
  ]
}Example curl Command:curl -X POST http://localhost:5000/recommend \
-H "Content-Type: application/json" \
-d '{
  "current_profile": {
    "country": "Australia",
    "topics": ["Technology", "Economics"]
  }
}'RequirementsPython 3.xFlaskscikit-learnpandasnumpyInstall dependencies:pip install Flask scikit-learn pandas numpyRunning the ApplicationSave the code to a file named app.py.Run the application:python app.pyThe server will start on http://localhost:5000.NotesEnsure you run the /train endpoint with the correct data before calling /recommend.The model and encoders are saved in people_recommender_model.pkl. Ensure the file is accessible by the Flask app.Adjust the data and model parameters based on your specific use case for improved performance.For further customization or improvements, consider incorporating more advanced machine learning techniques or adding additional features to the model.
