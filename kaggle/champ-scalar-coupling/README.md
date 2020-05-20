=======
# Predicting Molecular Properties kaggle competition

## Summary 
 - Objective: develop an algorithm that can predict the magnetic interaction between two atoms in a molecule (i.e., the scalar coupling constant)
 - Evaluation metric: log of MAE
 - My modeling pipeline:
    **Data Exploring -> Data Preprocessing -> Model selection -> Model Training -> Model Evaluation -> Submission**
 - Competition link: https://www.kaggle.com/c/champs-scalar-coupling/overview/description
 
## Pipeline of Modeling
 - Data Exploring
   - I used several different techniques to quickly gain some insights of these datasets 
   - For example, df.corr() can provide us with correlation among features; df.info() tells us how many non-null values that each feature has, etc
   - I did some basic data cleaning, which was either drop null values or fill null values with the mean of that feature.
 - Data Preprocessing
   - There are several different datasets that are related to molecule's type and atom's types, as well as distance between each atom in a molecule. Thus, I merge all the dataset to train.csv, which is the major dataset, by using df.merge_asof(), df.join(), etc. 
   - After merging, the dataset becomes quite large. Therefore, I create a function to reduce the memory usage of this dataset, and it is also helpful for the next step: feature engineering and transformation.
   - Feature engineering: extract more important features such as distance between atoms and the center of molecules, ionization energy, and electronegativity of each molecules. 
   - Feature Transformation: I used StandardScaler() for transforming numerical data and OneHotEncoder() for transforming categorical data.
 - Model Selection and Training
   - Using Stochastic Gradient Descent Regressor since the dataset is quite large, it can help us reduce the time cost.
   - Random Forest with bayesian optimatization (I tried randomized search for tuning hyperparameters, but it has lower score than bayesian optimization.)
   - lightgbm regressor (used some open source codes)
 