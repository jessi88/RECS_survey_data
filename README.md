#  Predict electric consumption using the Residential Energy Consumption Survey (RECS) data

## 2009 RECS Survey Data
[Source](https://www.eia.gov/consumption/residential/data/2009/index.php?view=microdata): "This 2009 version represents the 13th iteration of the RECS program. 
First conducted in 1978, the Residential Energy Consumption Survey is a national sample survey that collects energy-related data for housing units occupied as a 
primary residence and the households that live in them. Data were collected from 12,083 households selected at random using a complex multistage, 
area-probability sample design. The sample represents 113.6 million U.S. households, the Census Bureau’s statistical estimate for all occupied housing units in 
2009 derived from their American Community Survey (ACS).

Data are available in two formats: CSV, a comma delimited file and a SAS data file. The comma delimited data file is accompanied by a corresponding "Layout file", which contains descriptive labels and formats for each data variable. The "Variable and response codebook" file contains descriptive labels for variables, descriptions of the response codes, and indicators for the variables used in each end-use model.

Users are strongly encouraged to read [Using the 2009 microdata file to compute estimates and standard errors (RSEs).](https://www.eia.gov/consumption/residential/methodology/2009/pdf/using-microdata-022613.pdf)"


## Deliverables
Build a model that predicts consumption. The electric consumption is located in the `KWH` field.


## Data Preparation
The data has 940 columns and 12,083 rows. Data cleaning is crucial to reduce the number of dimensions.
- Remove variables which are referred to as "imputation flags".
- "Variables that were not imputed use the response codes -9 for `Don't Know` and -8 for `Refuse`. 
Variables that are not asked of all respondents use the response code -2 for `Not Applicable`". 
For our prediction task and due to limited time available, we replace the -2, -8, and -9 responses with the median values of each column. 
- There is a perfect positive correlation between our target `KWH` and `BTUEL`, so we drop `BTUEL` and related variables.
- Remove multicollinearities and biased responses.
- Remove outliers using the z-score<3 rule.
- Apply a log-transformeation to skewed variables.
- Convert the categorical variables into dummy/indicator variables.

## Modeling
- Split the data into random train and test subsets.
- Perform Sequential Feature Selection to obtain the "best" 25 features.
- Perform linear regression.

## Evaluation
- R2 Score on the test set: 0.821602
- RMSE on the test set: 0.274240
- The p-values indicate that all selected features are significant.

## Next Steps:
- Better understanding of the variables
- More careful handling of Don't Know/Refuse/Not Applicable responses
- Identify nominal categorical variables (no intrinsic ordering)
- Outlier treatment
- Nonlinear features and interactions between variables
- Principal component analysis (PCA)
- Combine similar categories
- Compare other regression models, such as tree models
- Clustering to identify subsets on which regression may/should be performed separately

## Link to Notebook

[RECS_survey_data.ipynb](https://github.com/jessi88/RECS_survey_data/blob/main/RECS_Survey_Data_2009.ipynb)
