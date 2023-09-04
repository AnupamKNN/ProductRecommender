### ProductRecommender

### Software & Tools Requiremntts

1. [Github Accounts](https://github.com)
2. [GitCLI](https://git-scm.com/)
3. [Anaconda](https://www.anaconda.com/)
4. [VS Code IDE](https://code.visualstuido.com/)


Create a new environment
```
conda create -p venv python -y
```

Assign User Name

```
git config --global user.name "Your name"
```

Assign Email used to create Github Account

```
git config --global user.email "You@example.com"
```

Install ipykernel within the environment in the terminal before running jupyter notebook.

```
pip install ipykernel
```

### Introduction (Problem Statement)
The aim of this project is to create a suggestive model which will suggest top 5 products for the investment bracket, with detailed report sentiment analysis on those product reviews.

### Dataset information

The dataset used for this project was 'Amazon 5-score Home & Kitchen reviews' which was obtained from Kaggle. A google drive link is also attached in the python notebook which also contains the dataset.

### Loadint the dataset

1. Here, gzip library was introduced first.
2. A function 'parse' was created with 'path' as the parameter.
3. The gzip algorithm was used to open the file stored in 'path' location in 'rb' (read binary) to open the file in binary mode.
4. A function 'getDF' as defined & 'path' parameter was passed to it.
5. A dictionary 'df' was created within the function which will store the data from the file stored in 'path' location.
6. getDF function was applied to the file and was stored in 'df'


### Data Dict

The above dataset has 9 variables. Those are:-

1. reviewerID: ID of the reviewer 
2. asin: ID of the product  
3. reviewerName: Name of the reviewer
4. helpful: helpfulness rating of the reviewer, e.g: 2/3
5. reviewText: text of the review
6. overall: rating of the product
7. summary: summary of the review
8. unixReviewTime: time of the review (unix time)
9. reviewTime: time of the review (raw)

### EDA
1. df.shape is used to check the number of rows and columns in 'df' data frame.
2. Two new columns 'helpfulfirstelement' & 'helpfulsecondelement' were created & 'helpful' column was dropped.
3. Again, the shape of the df wac checked to make sure that the 2 new columns were created & stored in the dataframe.
4. A new data frame 'reviews_count' was defined which contained the count of the reviews using 'groupby' function grouped by 'asin' feature.
5. A new data frame 'df_merged' was created & data frames 'df' & 'reviews_count' were merged using 'right-join' with 'asin' as a common column within both the data frames.
6. Columns in df_merged were renamed using ('reviewerID_y': 'reviews_count', 'overall_x': 'overall_review', 'summary_x': 'summary_review') names.
7. Now, the values of df_merged were sorted using 'sort_values' function on the basis of 'reviews_count' in descending order to sort the values from highest to lowest.
8. A new data frame 'df__review_mean' was created where the mean value of all the features of the data frame was deduced using 'groupby' function with all the data points grouped on the basis of 'asin' feature.
9. A new data frame 'df_summary_review' was created which contained all the reviews o eacg product using 'groupby' function grouped on the basis of 'asin' feature.
10. A new data frame 'df_model' which has 'df_summary_review' & 'df_review_mean' merged together using 'pd.merge'.
11. A new data frame 'df_model_data' was created which stored 'asin', 'summary_review' & 'overall' features from 'df_model'


### Text processing for modeling

1. A function 'text_process' was created with text as passed parameter for preprocessing text data within the data frame before training the model.
2. A new column 'clean_summary_review' was created in the 'df_model_data' data frame which stored string of all the text in df_model_data['summary_review'] with any single word or sentence replaced by an underscore.
3. The duplicate values were dropped from the data frame using 'drop_duplicate' function & the index of the data frame were reset using '.reset_index()' function.
4. A 'tfidf' model was created with 'TfidfVectorizer' algorithm & then 'clean_summary_review' from df_model_data was passed for fitting and transroming the data for the model. This fitted model was stored in 'X'
5. X is now split into training and testing data sets with 80& data for training & remaining 20% data for testing.

### Predictive Modeling

1. KNerighborsClassifier was used to classify: Predicting overall review based on product reviews.
2. The target variable for predictive modeling.
3. The code starts by creating a list of the overall data. This is done with df_model_data['overall'].
4. Then, it creates two variables: X_train and y_train.
5. These are lists of all the training data for this model.The first variable, X_train, has shape[0] equal to 10 because there are 10 rows in that list.
6. The second variable, y_test, has shape[0]: 9 because there are 9 columns in that list.
7. Next, it creates an array called xy which contains all the features from both arrays (X and Y).
8. The K-Neighbours-Classifiers algorithm was declared using 'neighbors.KNeighborsClassifier' & training data (X_train & y_train) was passed to the model for fitting the data & training the model.
9. After training the model, the accuracy of the model was deduced which turned out to be 89.49%.
10. The mean squared error of the model was also deduced which was about 10.50%

### Word Clouding for each review group
