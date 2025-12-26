**From a Global Stacked Model to Indian Football (ISL)**

*📌 What this project is about*

  This project builds a global Expected Goals (xG) prediction model using shot-level football data and then adapts it for Indian football (ISL).
  Instead of creating a brand-new xG model only from ISL data (which is limited), the idea is to:
  
   - first learn general shot-scoring patterns from a broader dataset
    
   - then adjust those predictions using Indian football–specific context
    
   - This makes the model both data-efficient and football-aware.

*🧠 Core Idea (in simple terms)*

  A shot taken from the same location does not always have the same difficulty in every league.
  
  So the project:
  
   - Builds a strong global xG baseline
    
   - Combines multiple models using stacking
    
   - Uses a meta-model to recalibrate predictions using contextual features

Applies this setup to Indian Super League (ISL) shots

🗂️ Repository Structure
├── Extracting_ISL.ipynb
├── ISL_shots_feature_engineering.ipynb
├── Xg_Model.ipynb
└── README.md

📁 Notebook Explanation
  1️⃣ Extracting_ISL.ipynb — ISL Shot Data Extraction
  
  Goal:
  Collect and organize Indian Super League shot data in a usable format.
  
  What happens here:
  
   - Match and shot-level events are extracted
    
   -  Only relevant shooting events are retained
    
   - Data is cleaned and reshaped for modeling
  
  Output:
    A structured dataset containing ISL shots with spatial and contextual information.
  
  2️⃣ ISL_shots_feature_engineering.ipynb — ISL-Specific Features
  
  Goal: Make the ISL data compatible with a global xG model while preserving league context.
  
  Key steps:
  
   - Standardizing shot attributes (body part, shot type, etc.)
    
   - Handling missing or inconsistent values
    
   - Creating clean, model-ready features
    
  Why this matters:Feature consistency is crucial when global models are applied to local leagues.

  3️⃣ Xg_Model.ipynb — Global xG Model & Stacking (Main Notebook)

  This is the core of the project.
  
  🔹 Baseline xG Modeling
  
  The target variable is expected goals (xG), treated as a continuous probability.Models are trained using spatial and shot-related features.The goal outcome (0/1) is never used as an input feature
  
  🔹 Base Models
  
  Multiple base learners are trained independently, each capturing different patterns in the data.
  (Tree-based models are especially effective for spatial football data). Each base model outputs a predicted xG value for every shot.
  
  🔹 Stacked Ensemble
  
  Predictions from all base models are combined.These predictions become inputs to a meta-model.The meta-model learns:
  
  - how much to trust each base model
    
  - how to correct systematic bias in predictions
  
  This improves: stability, generalization, probability calibration
  
  🔹 Context-Aware Meta Modeling
  
  To adapt the model for Indian football: The meta-model is also fed contextual football features. These features help recalibrate xG values for league-specific conditions. 
  This allows the model to adjust global xG predictions without retraining everything from scratch.
  
  🔹 Evaluation Strategy
  
  The model is evaluated from two perspectives: Regression Metrics, Mean Squared Error (MSE), Mean Absolute Error (MAE), R² Score → measures how close predictions are to reference xG values.
  And Probability Metric  Brier Score and  Log Loss → measures how well predicted xG matches real goal outcomes. Cross-validation is used to ensure the model is robust and not overfitting.
  
  📊 Why This Approach Works
  
  Uses strong global learning instead of limited local data.Avoids target leakage.Treats xG correctly as a probability, not just a label.Reflects how modern football analytics models are built in practice
  
  🚀 Possible Extensions
  
  Shot calibration plots.Team- and player-level finishing analysis.Match-state and defensive pressure features.Interactive dashboards for analysts or coaches
  
  *🏁 Final Note*
  
  This project is not just about predicting goals.
  It focuses on how to transfer football knowledge across leagues, using stacking and contextual modeling — a key challenge in real-world sports analytics.
