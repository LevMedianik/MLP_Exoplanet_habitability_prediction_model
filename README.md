# MLP_Exoplanet_habitability_prediction_model 🌎🌱
This is Multi-Layer Perceptron model for exoplanet habitability prediction. The model is using NASA Exoplanet Archive dataset that includes more than 38000 planets and 66 variables reflecting planetary and stellar characteristics. The model can predict planet habitability with the accuracy of 99.67%. 
Data can be achieved in https://exoplanetarchive.ipac.caltech.edu/cgi-bin/TblView/nph-tblView?app=ExoTbls&config=PS.
This work can be deployed in Google Colab only.
Various feature engineering techniques and data augmentation steps were implemented to enhance model performance, ensuring accurate habitability classification.
# Working process of the model
## 1. Data Collection and Preprocessing
The dataset was obtained from the NASA Exoplanet Archive, containing planetary and stellar parameters.
Handling Missing Data:
Features with more than 50% missing values were removed.
K-Nearest Neighbors (KNN) Imputation was applied for features with less than 50% missing values to retain useful information.
Feature Encoding:
Categorical variables such as planet type and discovery method were encoded into numerical form for compatibility with the model.
## 2. Data Augmentation
To enrich the dataset and improve classification accuracy, additional astrophysical features were derived using fundamental physical laws:

Semi-Major Axis Calculation: Using Kepler’s Third Law, estimating a planet’s distance from its star.
Equilibrium Temperature: Determines the planet's radiation balance based on stellar temperature and radius.
Surface Temperature Estimation: Incorporates the greenhouse effect, varying based on planet size.
Planet Size Categorization: Classifies planets as Earth-like, Super-Earth, or Gas Giant based on their radius.
Thermal Categorization: Planets were grouped into Hypopsychroplanets, Psychroplanets, Mesoplanets, Thermoplanets, and Hyperthermoplanets based on their estimated surface temperatures.
## 3. Binary Habitability Classification
A planet is considered potentially habitable if it falls within the following criteria:
Size Category: Earth-like or Super-Earth.
Thermal Category: Psychroplanet, Mesoplanet, or Thermoplanet.
The function classify_habitability() assigns each planet to either "Potentially Habitable" (1) or "Not Habitable" (0) based on these conditions.
## 4. Data Balancing using SMOTE
Due to the severe class imbalance in exoplanet habitability labels, Synthetic Minority Oversampling Technique (SMOTE) was applied to ensure a balanced dataset, preventing the model from being biased toward non-habitable planets.
## 5. Feature Scaling & Normalization
The dataset was normalized using StandardScaler, ensuring that all numerical features were on a consistent scale for efficient training.
## 6. Deep Learning Model: MLP Architecture
A Multi-Layer Perceptron (MLP) was designed with the following structure:
Input Layer: Takes in normalized features.
Hidden Layers:
five hidden layers with 128, 128, 64, 32, and 16 neurons, respectively.
ReLU activation function for non-linearity.
Dropout (0.3) applied to prevent overfitting.
Output Layer:
A single neuron with sigmoid activation for binary classification.
Compilation:
Loss Function: Binary Crossentropy.
Optimizer: Adam with a learning rate of 0.003.
Early Stopping: Prevents overfitting by monitoring validation loss with a patience of 5 epochs.
## 7. Model Training & Evaluation
The dataset was split into training (80%), validation (10%), and test sets (10%).
Training was performed over 50 epochs with batch size 32.
Model Evaluation Metrics:
Accuracy: Measures overall correctness of predictions.
Precision & Recall: Evaluates classification performance on the minority class.
Confusion Matrix: Visualizes false positives and false negatives.
AUC-ROC Curve: Assesses the model’s ability to distinguish between habitable and non-habitable planets.
## 8. Model Performance & Results
The **classification report** indicated a high level of accuracy with balanced precision and recall:
![image](https://github.com/user-attachments/assets/45bcab32-02e5-4e10-a5db-1a79b1649b2b)

The **confusion matrix** showed that the model effectively classified the majority of **potentially habitable** exoplanets correctly.  
![image](https://github.com/user-attachments/assets/1950822a-0154-4c60-81d1-4039bcdf2208)

The **AUC-ROC curve** displayed near-perfect discrimination between habitable and non-habitable planets.
![image](https://github.com/user-attachments/assets/331f350a-fcff-4f31-a2d5-6a08620a5d2c)

The **learning curves** demonstrated a good fit of the model
![image](https://github.com/user-attachments/assets/1b53eaa9-a2fe-4fdb-94de-8e1b185d889e)

## References
1. NASA Exoplanet Archive: https://exoplanetarchive.ipac.caltech.edu/
2. Mathur, S., Sizon, S., & Goel, N. (2021). Identifying Exoplanets Using Deep Learning and Predicting Their Likelihood of Habitability.
3. LeCun, Y., Bengio, Y., & Hinton, G. (2015). Deep learning. Nature, 521(7553), 436-444.
