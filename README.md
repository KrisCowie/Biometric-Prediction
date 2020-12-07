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

Then run the notebook, it will produce a highly accurate chained random forest model of the biometrics

The notebook takes the dataset, and uses the weights associated with the 16,000 individuals to upsample to 100,000.

Then we identify the target variables, and build a chained random forest regressor model, and use it to predict our variables.

We use Chained Random Forest as it takes into account the relationships between the features you want to predict - things like HDL and LDL, Apolipoprotein and LDL, etc carry inherent associations, which would be lost if you just did a series of models that predicted each of the features based on Age, Gender, Height, and Weight.
