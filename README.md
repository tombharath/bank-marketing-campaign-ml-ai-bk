# Bank Marketing Campaign
This is a practical application assignment to compare the performance of the classifiers k-nearest neighbors, logistic regression, decision trees, and support vector machines. 

**Context**

The dataset is related to the marketing of bank products over the telephone. The dataset comes from the UCI Machine Learning repository [link](https://archive.ics.uci.edu/ml/datasets/bank+marketing). 
The data is from a Portugese banking institution and is a collection of the results of multiple marketing campaigns.

**Code**

- Refer to [prompt_III.ipynb](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/blob/main/prompt_III.ipynb) jupyter notebook for the code.
- The code uses Plotly express libraries. As GitHub doesn't display plotly chart correctly. The renderer is used to show it as a picture.
- You can change the fig.show("png") to fig.show() in the jupyter notebook python code to have the hover functionality while running it.

**Business Objective**

The business objective is to find a model that predicts if the client subscribes to the deposit by identifying the main characteristics that lead to the success. 
This type of model can help marketers to have a targeted campaign so that marketing resources can be better used towards the client more likely to subscribe.

**Data Understanding**

- The dataset collected represents 17 phone marketing campaigns between May 2008 and November 2010. 
- The goal is to get them to subscribed to the long-term deposit application by marketing them with good intrest rates.The dataset has success rate of 8 %.
- Below is the summary of the data to understand the categorical and numeric features in the data set.

![Screenshot 2024-06-03 at 3 30 05 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/460e067e-e9ab-4308-8eac-6cfd5e272aad)

**Data Preparation**
- There are no missing values in the dataset
- There are 12 duplicates and it is removed as dataset has 400K records.

**Data Preprocessing**

- Renamed the y column to target variable subscribed and converted the Binary column into Numerical
- Used Ordinal Encoding to convert Categorical education column to numeric
- Converted the rest of the nominal Categorical Column to Numeric Using Mean Encoder
- The dataset is imbalanced based on the subscribed feature.

![Screenshot 2024-06-03 at 3 34 14 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/4d50a46f-1b4d-4ab8-a2e9-fa275dc8b5d7)

- Splitted the dataset for train and test set with 70 % ratio.
- Scaled the dataset
  
**Modelling**

The following models has been evaluated to compare the performance

- Logistic Regression
- KNN Algorithm
- Decision Tree
- Support Vector Machines (SVM)

**Baseline Model**

- The accuracy of the Baseline classifier for train dataset is 88.85%
- The accuracy of the Baseline classifier for test dataset is 88.47%

**Model Comparision**

Below is the performance of the each models with the default settings of each model.

![Screenshot 2024-06-03 at 3 38 40 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/c1b31d96-4146-4658-82b1-4bd009b65f8e)


**Model Tuning**

- Feature Engineering and exploraion using heat map provided the below insights
    - The subscribed feature is having a similar positive correlation
        - Between cons.conf.idx and martial and loan
        - Between previous and month
        - Between days_of_week and age
        - Between contact and job
    - The subscribed feature is having a similar negative correlation
        - Between euribor3m and emp.var.rate
        - Between nr.employed and pdays
    - The subscribed feature is having a similar inverse correlation
        - Between poutcome and euribor3m
        - Between poutcome and nr.employed
        - Between poutcome and emp.var.rate
  
  ![Screenshot 2024-06-03 at 3 42 31 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/d8acf0f0-7e3a-4793-ba86-137612dce49c)

 - SequentialFeatureSelection is used to select the 9 features which represent these collinearity of the dataset and to avoid multicollinearity with each other
     - age
     - job
     - marital
     - default
     - housing
     - campaign
     - pdays
     - poutcome
     - nr.employed
  - The dataset with only the above features are used for the model further analysis
  - Below are the tuning parameters used for each of the models
      - Logistic Regression
         - max_iter=[10000]
         - c=[0.001,0.01,0.1,1,10]
         - penalty=['l1', 'l2']
       - KNN Algorithm
         - knn__n_neighbors = list(range(1, 25, 2))
      - Decision  Tree
         - criterion = ['gini','entropy'],
         - min_samples_leaf = range(1,10)
      - Logistic Regression
         - kernel_range = ['linear', 'poly', 'rbf', 'sigmoid']
  - The GridseachCV with recall scoring is used to get the the best parameters
  - Used recall as scoring as missing out on the potential subscribed customer will impact the business goal.
  - Below is the summary of the performance of models after tuning

    ![Screenshot 2024-06-03 at 3 51 09 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/9a2ed7d9-59c1-4284-b08d-e04798179136)

  - Below is the ROC Curve of each Model

    ![Screenshot 2024-06-03 at 3 52 04 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/4b16b4ca-f579-4232-b6fd-b9a3b61476ab)

**Model Evaluation**

- The Model is tuned for hyperparameters based on the recall score.
- Used recall as scoring as missing out the potential subscribed customer will impact on the business goal
- Based on the Model Analysis the Logistic Regression, Decision Tree and SVC has better test score of 89 %
- The Training Time of the SVC is much higher compared to the Logistic Regression and Decision Tree
- The ROC Curve shows the logistic regression has a better trade-off between the Precision and Recall.
- Logistic Regression Classifier seems to be better for the given dataset in the case of the performance parameters.

## Observations

Permutation Importanace of Logisitic Regression Model revels the top four features that impacts the customer will subscribe to the deposit account or not are below
- pdays
- nr.employed
- campaign
- age
  
**pdays**
- The number of days that passed by after the client was last contacted from a previous campaign (numeric; 999 means client was not previously contacted)

  ![Screenshot 2024-06-03 at 3 55 31 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/8ee61a21-a68c-4444-bf4e-414f1ad72392)

**Number of Employees**
- The number of employees
  
![Screenshot 2024-06-03 at 3 55 57 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/165aa134-7b98-41d2-8c18-9970f0a0163b)

**Campaign**
- The number of contacts performed during this campaign and for this client (numeric, includes last contact)

  ![Screenshot 2024-06-03 at 3 56 23 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/19bc9b4d-174e-4c6c-b3b8-8306b3eeb84f)

**Age**
- The Age of the contact

  ![Screenshot 2024-06-03 at 3 56 45 PM](https://github.com/tombharath/bank-marketing-campaign-ml-ai-bk/assets/37302704/b04d5c31-3426-43fd-a2eb-fbee600387a4)

## Recommendation and Next Steps

- The targeted marketing campaign can focus on below observations to have a high successful rate of subscription to the deposit.
  - Making the contact again between 3 and 6 days after the last contact has a high success rate
  - More Contact has been made for the number of employees > 5100 however the comparitieve success rate is higher for the < 5100 number of employees.
  - Targeting the < 5100 number of employees is having a higher success rate.
  - The Success is higher if the contact is done less than 5 times for the campaign. More number of contacts has less success rate of subscription
  - The Age group of < 40 has high success rate.
- Gather the dataset with higher success rate to crossverify and retrain the models


  


  
