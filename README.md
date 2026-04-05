# **CS-SINS Models**

This repository contains all the datasets and code used to train models in the CS-SINS paper.


The folder "Classifier" contains the code to train the decision tree found in Figure 5. The folder "Regressor" contains the code and data used to train and test the support vector regressor found in Figure 6.

## **Running the Classifier Model**

To run the classifier model, physicochemical properties need to be calculated at **pH 6** using Molecular Operating Environment. For best results, we recommend using average porperties from 5 predicted structures per antibody.

*Step 1 - Install dependencies*

The classifier was trained in Python version 3.10. All dependencies are listed in requirements.txt in the classifier folder. 

*Step 2 - Run the model*

The following code can be used to run the model.

```python
import pandas as pd
import joblib

# read in the dataframe with properties from MOE
df = pd.read_csv(<path to csv files containing properties>

# import the model
model = joblib.load('CSSINS_Classifier.pkl')

# predict CS-SINS
X = df[[app_charge, zquadrupole]]
predictions = model.predict(X)
```

Note that the input to the model should be a Pandas Dataframe with the following format:

|app_charge|zquadrupole|
|:------:|:------:|
|...|...|

## **Running the Regressor Model**

To run the regressor model, physicochemical properties need to be calculated at **pH 6** using Molecular Operating Environment. For best results, we recommend using average properties from 5 predicted structures per antibody.

Additionally, the Format column should be filled out such that **0 = IgG1 Fc** and **1 = IgG4 Fc**.

*Step 1 - Install dependencies*

The regressor was trained in Python version 3.9. All other dependencies are listed in requirements.txt in the regressor folder.

*Step 2 - Run the model*

The following code can be used to run the model

```python
import pandas as pd
import joblib

# read in dataframe with properties from MOE
df = pd.read_csv(<path to csv files containing properties>)

# import the model
model = joblib.load('CSSINS_Regressor.pkl')

# predict CS-SINS
X = df[['zdipole', 'hyd_moment', 'pI_3D', 'patch_ion_1', 'Format']]
predictions = model.predict(X)

```

An example from the training and testing  **CS-SINS_regression.ipynb**.

Note that the input to the model should be a Pandas Dataframe with the following format:

|zdipole|hyd_moment|pI_3D|patch_ion_1|Format|
|:-----:|:--------:|:---:|:---------:|:----:|
|...|...|...|...|...|

