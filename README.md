# Biometric-Prediction
Predicting biometrics from CDC NHANES data

CDC NHANES data provides a complex survey sample of the non-institutionalized population of the United States every 2 years.

Individuals go through a battery of lab tests for everything from LDL and HDL to Perchlorates, Pesticides, along with wide ranging demographic and body measurement data.

If you wanted to predict biometrics like LDL, HDL, blood pressure / sugar, triglyercides, etc. just from an individuals age, gender, height, and weight, how would you go about it?
Well, a little something like the chained random forest regressor model in this repo.

First datasets are downloaded from the CDC's website:
https://wwwn.cdc.gov/nchs/nhanes/Default.aspx

Each individual is given a weight (indicating the number of people they represent in the non-institutionalized population of the United States)

This weight changes based on which tests they participated in (the fasting sub sample, for example, tested less people than they were able to get to respond to the demographic questionnaire, so there's different weights associated with these people).

Identify the datasets you need (APOB, BIOPRO, BMX, BPX, DEMO, GHB, GLU, HDL, TCHOl, and TRIGLY) for each year (in this case I used 2005-2016)

Create a merged dataset which retains the weight of the individual, along with the pertinent features.

The dataset has already been cleaned and assembled previously, so it's got the pertinent weights for each individual, and has non necessary data points dropped.

Using bayesian optimization, and hyper opt packages, we can loop over each iteration of the model, and select the best hyperparameters for predicting each biometric.

Once the best hyperparams are discovered, we can create a model fitting loop which grabs the correct hyperparams from a dictionary for each loop, depending on which biometric we're prediciting.
Put it all together, and you eventually save 10 models, one each for the labels we're looking for.

Then we save each model with a unique name, and use them to make predictions on CDC NHANES data from 2017-2018, which the model hasn't seen before.

Anndd that didn't work very well.
Our Mean Absolute Error turned out to be pretty mediocore.

So back to the drawing board! Think it might be pertinent to use a chained regressor which will take into account the correlations between predictor variables.
 
