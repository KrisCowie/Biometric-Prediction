# Biometric Prediction
Biometric predictions based on 12 years of CDC NHANES data:

Predicts: 
- Waist Circumference 
- Systolic / Diastolic blood pressure
- HDL
- LDL
- Triglycerides
- Serum glucose
- Glycohemoglobin
- Plasma glucose
- Apolipoprotein

From only 5 features:
- Age, Gender, Height, and Weight

Took a couple of different approaches to this problem - random forest regression was likely to be the best, but tested Tab Net Neural Networks, and some custom code to produce first a) tweak the hyperparameters of each feature for Light GBM, and then b) multiple output LightGBM, as LightGBM's implementation in Python doesn't support native multi-output

Both of these produced good, but not great results, so the final model used a Random Forest Regression model, upsampling the initial dataset of 16,000 to ~500,000, based on the weights assigned to them in the complex survey method the CDC employed to gather the data in the first place.

These weights were immensely helpful to creating an accurate model as sort of meta-weights for the model

The final model / script are set to private, message me if you'd like to see more!

Final script produces the model after preprocessing and upsampling the dataset, then the second script will take in a CSV called 'data.csv', and first calculate BMI, then run the model against it, predicting the 10 labels we want, followed by classifying each prediction, i.e.:
BPSYAVG - Low, Normal, High, High Stage 2 blood pressure
BPDIAVG - Low, Normal, High
Glycohemoglobin - Normal, Prediabetic, Diabetic

Etc. You could work the problem as a classification problem, and likely have better 'accuracy', but I thought working it as a regression problem would allow more precise estimation of the biometrics

So back to the drawing board! Think it might be pertinent to use a chained regressor which will take into account the correlations between predictor variables.
 
