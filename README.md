# Using Machine Learning to Detect Fraudulent Transactions
## Group Members
Nicholai Shaw, Jessica Morris, Zachary Kroell, Chris Moeglin, and Timothy Coleman

## Background
Recent data from the Federal Trade Commission (FTC) show that consumers lost nearly $8.8 billion to fraud in 2022 ("*New FTC data*," 2023). The FTC received fraud reports from 2.4 million consumers, most of whom were targeted by imposter scams, followed by online shopping scams. These data show that fraudulent transactions impose a massive burden on Americans across the country, so we created a supervised machine learning model to better predict fraudulent transactions to aid in the process of detecting and stopping scams. To accomplish this goal, we used a dataset from Kaggle that possessed 111,144 credit card transactions that were classified as either fraudulent or not fraudulent (Shenoy, n.d.). After creating the models, we also wanted to visualize which fraud categories had a higher occurance and where the greatest amounts of frauds occur using Tableau. 

## Data Exploration
The raw dataset from Kaggle contained a random sample of 111,144 credit card purchases. Various features of each credit card purchase were included in the dataset: credit card number, transaction id, gender of card holder, first and last name of card holder, merchant name, transaction category, amount of transaction, geographic information (latitude, longitude, street name, zip code, city, state), date of birth, and time and date of transaction. Using these data, we created two models—a logistic regression and random forest—to predict instances of fraud.

## Data Cleaning
Before creating the models, we had to clean the data so it can be read. First, we exported the data from a csv file to a pandas dataframe. 

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/f7791125-8fc0-4ab8-af9e-53919e589bae)

**Figure 1.** *Snapshot of the raw dataset.*

Next, we renamed the 'Unamed: 0' to 'transaction_id' and 'amt' to 'amount.' After the columns were renamed, we separated the transaction date and time in the column 'trans_date_trans_time' to two separate columns: transaction date and transaction time.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/205a9968-a610-4c0a-af71-f78ca6d00ad4)

**Figure 2.** *Transaction date and time separated.*

After the transaction date and time were separated, we converted date of birth into age using the datetime library.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/d88245b9-aeb3-4c3f-aa16-c93e8d623390)

**Figure 3.** *Conversion of date of birth into age.*

Lastly, the columns were reordered, and then we dropped the columns that were not features of the model.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/3a69009b-02b4-4295-af80-c6ae3b7f09de)

**Figure 4.** *Columns that were not features of the model were dropped to ensure accuracy of the prediction.*

## SQLite Database
A SQLite database was used to house the clean data. SQLAlchemy was used to connect the clean pandas dataframe to the database. Transaction ID was used as the primary key in the SQLite database.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/a796f3c0-f6e0-4d99-b0cf-afba9ea70c6e)

**Figure 5.** *SQLite connection between the pandas dataframe and the database.*

## Logistic Regression
### Model Creation
We imported the data from the SQLite database to a pandas dataframe using SQLAlchemy. We dropped the transaction id since it is not a feature of the regression. Lastly, we used the pd.get_dummies function to transform the categorical data in the dataframe to numeric.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/1bcf5f48-e111-4e15-bb6d-c27917ec8531)

**Figure 6.** *The use of pd.get_dummies to transform the categorical data into numeric.*

Next, we separated the features and the labels. the labels were noted as 'y,' and the features were notated as 'x.'

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/4df850ec-bbff-4b1b-adc4-2e6839b4f0c9)

**Figure 7.** *Separating the features and labels in the regression.*

Lastly, we split the data into training and testing sets and scaled the data for precision. We reserved 20% of the data to the testing set.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/cb02a99d-8b9e-4e31-9f3d-3b1cfc1219e4)

**Figure 8.** *Splitting into training and testing sets.*

### Model Compiling
The linear regression model was complied using the sklearn library.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/6ff2b0be-e51c-4c37-ab4f-710cbf5af44f)

**Figure 9.** *Model compiling using the sklearn library.*

### Model Performance
The balanced_accuracy_score function revealed a balanced accuracy score of 53.1%. This means that the model performs slightly better than random chance to predict fraudulent and non-fraudulent cases.<br>
</br>The confusion matrix showed a high amount of correctly predicted non-fraudulent cases (22164) and low amount of incorrectly predicted fraudulent cases (2). The model also showed very few true fraudulent cases (4) and a high amount of false negatives (59). The confusion matrix highlights a significant imbalance in the groups—with a much larger proportion of non-fraudulent cases compared to fraudulent cases. This poses challenges for the model's ability to accurately predict fraud.<br>
</br>The precision was high for valid purchases and moderately low for fraudulent (100% and 67% respectively). This means that the model was 100% correct when predicting the non-fraudulent purchases but only 67% accurate when predicting the fraudulent cases. Recall was high for valid purchases and very low for fraudulent (100% and 6% respectively). This means that the model successfully identified all non-fraudulent purchases 100% of the time. However, the model only detected 6% of the actual fraudulent cases.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/dc5e66cc-ccfa-40a0-bf5b-8d233ef215d9)

**Figure 10.** *Logistic regression performance metrics: balanced accuracy score, confusion matrix, and classification report.*

## Random Forest
### Model Creation and Model Compiling
Similar to the logistic regression model, data were imported to a pandas dataframe fromt he SQLite database using SQLAlchemy. The transaction ID column was dropped since it is not a feature of the analysis. We used pd.get_dummies to transform the categorical data to numeric.<br>
</br>We then separated the features and labels and split the data into training and testing sets. We allocated 20% of the data to the testing set.
### Model Performance
The balanced_accuracy_score function revealed a balanced accuracy score of 79.3%—significantly higher than the logistic regression. This means that the model performs moderately better than random chance to predict fraudulent and non-fraudulent cases.<br>
</br>The confusion matrix showed a high amount of correctly predicted non-fraudulent cases (22164) and low amount of incorrectly predicted fraudulent cases (2). The model also showed few true fraudulent cases (37) and a low amount of false negatives (26). The confusion matrix highlights a significant imbalance in the groups—with a much larger proportion of non-fraudulent cases compared to fraudulent cases. This poses challenges for the model's ability to accurately predict fraud.<br>
</br>The precision was very high for both valid purchases and for fraudulent (100% and 95% respectively). This means that the model was 100% correct when predicting the non-fraudulent purchases and 95% accurate when predicting the fraudulent cases. Recall was high for valid purchases and low for fraudulent (100% and 59% respectively). This means that the model successfully identified all non-fraudulent purchases 100% of the time. However, the model only detected 6% of the actual fraudulent cases.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/75509d25-cd72-42ae-95ba-6cd21ca405e1)

**Figure 11.** *Random Forest performance metrics: balanced accuracy score, confusion matrix, and classification report.*

## Comparison of the Logsitic Regression and Random Forest
The balanced accuracy score was much higher in the random forest model (79.3%) than the logistic regression (53.1%). The confusion matrices showed a significant imbalance in the groups for both models. The confusion matrices showed that the random forest model predicted more correctly predicted fraudulent cases than the logistic regression (37 vs. 4) and fewer false negatives (26 vs. 59).<br>
</br>The precision for fraudulent purchases and non-fraudulent purchases in the random forest (100% and 95% respectively) was significantly higher than the precision for fraudulent purchases and non-fraudulent purchases in the logistic regression model (100% and 67% respectively). The recall scores for the fraudulent and non-fraudulent purchases in the random forest model (100% and 59% respectively) was significantly higher than the recall scores for the fraudulent and non-fraudulent purchases in the logistic regression model (100% and 6% respectively).

## Tableau
To provide further insight into the occurrence and prevalent categories of fraudulent cases, we utilized our clean dataset of 111,144 credit card transactions. We imported the data to Tableau and crafted a series of visuals and interactive dashboards to delve deeper into the complexities surrounding fraud detection.<br>
</br>Access to Tableau Dashboard: [Tableau Dashboard Link](https://public.tableau.com/app/profile/nicholai.shaw/viz/FraudulentTransactions_17096911116960/Story)

## References
*New FTC data show consumers reported losing nearly $8.8 billion to scams in 2022*. (2023, February 2023). Federal Trade Commission. Retrieved November 29, 2023, from https://www.ftc.gov/news-events/news/press-releases/2023/02/new-ftc-data-show-consumers-reported-losing-nearly-88-billion-scams-2022

Shenoy, Kartik. (n.d.). *Credit card transactions fraud detection dataset*. Kaggle. https://www.kaggle.com/datasets/kartik2112/fraud-detection?select=fraudTrain
