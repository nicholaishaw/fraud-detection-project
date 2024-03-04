# Using Artificial Intelligence to Detect Fraudulent Transactions
## Group Members
Nicholai Shaw, Jessica Morris, Zachary Kroell, Chris Moeglin, and Timothy Coleman

## Background
Recent data from the Federal Trade Commission (FTC) showed that consumers lost nearly $8.8 billion to fraud in 2022 ("*New FTC data*," 2023). The FTC received fraud reports from 2.4 million consumers, most of whom were targeted by imposter scams, followed by online shopping scams. These data show that fraudulent transactions impose a massive burden on Americans across the country, so we created a supervised machine learning model to better predict fradulent transactions to aid in the process of detecting and stopping scams. To accomplish this goal, we used a dataset from Kaggle that possessed 111,144 credit card transactions that were classified as either fraudulent or not fraudulent (Shenoy, n.d.). After creating the models, we also wanted to visualize which fraud categories had a higher occurance and where the greatest amounts of frauds occur using Tableau. 

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

Lastly, the columns were reordered and then dropped the columns that were not features of the prediction and ensure the data are analyzed correctly by the model.

![image](https://github.com/nicholaishaw/fraud-detection-project/assets/135463220/b9708a12-c450-4665-b80a-1f9cb179b7bd)

**Figure 4.** *Columns that were not features of the model were dropped to ensure accuracy of the prediction.*

## Logistic Regression
### Model Creation
### Model Compiling
### Model Performance

## Random Forest
### Model Creation
### Model Compiling
### Model Performance

## Tableau
After the models were created, we 
Access to Tableau Dashboard: [Tableau Dashboard Link](https://public.tableau.com/views/FraudulantTransactions/Dashboard1?:language=en-US&publish=yes&:display_count=n&:origin=viz_share_link)

## References
*New FTC data show consumers reported losing nearly $8.8 billion to scams in 2022*. (2023, February 2023). Federal Trade Commission. Retrieved November 29, 2023, from https://www.ftc.gov/news-events/news/press-releases/2023/02/new-ftc-data-show-consumers-reported-losing-nearly-88-billion-scams-2022

Shenoy, Kartik. (n.d.). *Credit card transactions fraud detection dataset*. Kaggle. https://www.kaggle.com/datasets/kartik2112/fraud-detection?select=fraudTrain
