# Final-Project-
This project is a classification task based on credit card transactions and whether they are considered fraudulent or not. It is essential that credit card companies keep track of whether a transaction is fraudulent so customers are not being charged for items they did not purchase. This dataset contains transactions from September 2013 by European cardholders. I pulled this dataset from Kaggle as it is something I have been looking at for years to do a project on, but never knew how. It consists of 284,807 rows, or transactions, and 31 columns, or features. The features are titles 'V1' ... 'V28' using PCA because of confidentiality, so we do not know what these features are, but they could include behavioral data, such as spending patterns, transaction times, and merchant types. The feature 'Time' refers to the nnumber of seconds elapsed between this transaction and the first transaction of the dataset. The feature 'Amount' refers to how much the transaction was in euros. Our response variable 'Class' refers to whether the transaction was percieved to be fraudulent(1) or not(0). This dataset was highly imbalanced with 99.83% classified as not fraudulent and 0.17% classified as fraud. It only contains numerical values because of the PCA transformation. 

Starting with Exploratory Data Analysis (EDA), we can load our dataset into the DataFrame 'creditcard' and display the first couple rows to understand the data's structure and contents. All of the variables are non-null meaning there are no missing values, and they are all floats, while 'Class' is an integer. We want to find the correlation of these variables, so we can use a sns heatmap to show us which variables are highly correlated with one another. We can see that 'V7' and 'Amount' are closest positive correlation with each other, so whichever feature V7 is has a moderately positive correlation with the amount of the transaction with 0.4. We can also see that 'V2' has a moderate negative correlation with Amount with -0.53. All of the other features seem to be somewhat correlated with the other hidden features. After plotting the sns heatmap, we can see if any correlation are more than 0.7 with either a True or False, which none of them are. To check for outliers in Amount and Time, we can look at their statistics and see that in 'Amount', the mean is 88.35, but the standard deviation is 250.12. This is quite a large spread meaning that the data is significantly spread out from the mean. With the minimum at 0 and the maximum at 25,691.16, this indicated extreme outliers or values. The same thing occurs within the variable 'Time'. We need to normalize the Amount and Time features because of their outliers using a MinMax Scaler. After scaling, we can see that the statistics have decreased to values between 0-1. The mean for Amount is now 0.0034 while the standard deviation is 0.0097, indicating a smaller spread within the data, eliminating any extreme values or outliers. Now, we can see which features are most strongly correlated with our target variable 'Class' by finding the top positive correlations and the top negative correlations. The top positive include 'V11', 'V4', 'V2', etc. with correlations of 0.155, 0.133, 0.091. The top negative include 'V10', 'V12', 'V14', and 'V17' with correlations of -0.217, -0.261, -0.303, -0.326. These preprocessing steps ensured our dataset was cleaner, more representative, and ready for modeling. 
![Outliers](https://github.com/user-attachments/assets/3a076426-b91b-4735-a7f7-c85f06e4f8ef)
![Stats After scaling](https://github.com/user-attachments/assets/e6292639-57e6-4964-a9c1-c0571b5a1f17)

![475-ConfMatrix](https://github.com/user-attachments/assets/a56239e7-18d7-4385-ad5e-6170a63f464d)

I chose to use a Logistic Regression model because of the classification task. The target variable is categorical with two classes and I wanted to estimate the probability of each class. I also used the XGBoost Classifier because it works well with classification tasks. Since my dataset was so large, XGboost is highly optimized and can train quickly and effienctly. It performs well is real-world scenarios, especially with predictive accuracy. I also included a Decision Tree to visualize how each feature splits the data. I found the XGBoost Classifier to be the most effective as it had to highest performance accuracy. 
![Imbalance](https://github.com/user-attachments/assets/d4fae288-0265-4169-b8a7-ee72205e699e)

When we plot the distribution between the classes, we can see that there is a significant imbalance with Class 0 being 99.83% while Class 1 is 0.17%. We will need to fix this imbalance using SMOTE. But first, we can select our features that are highly correlated with Class as our X, which are 'V11', 'V4', and 'V2', and our target variable 'Class' as y. We can scale our x and y to enhance the model performance by using StandardScalar. The results show that the x_train has 199,364 samples and 3 features, the x_test has 85,443 samples and 3 features, the y_train has 199,364 target labels corresponding to the training samples, and y_test has 85,443 target labels corresponding to the testing samples. Now, we can balance the dataset by using Synthetic Minority Oversampling Technique (SMOTE) by resampling our x and y and splitting the resampling into testing and training sets. This gives us a balance of 50%/50%. Using a Ranom Forest Classifier, we can improve the predictive performace and reduce any overfitting. The classification results after using SMOTE showed for Class 0, 100% precision, 99% recall, and 99% F1-score. For Class 1, it shows 99% Precision, 100% Recall and 99% F1-score. The accuracy is 99%. The resulting confusion matrix gives us 84,441 coreectly identified as No Fraud, 84,906 correctly identified as Fraud, 854 identified as Fraud, but were actually No Fraud, and 388 identified as No Fraud, but was actually Fraud. Since this is a classification task, we can use Logistic Regression with our SMOTE variables. We can see that the classification report gives us for Class 0 (No Fraud) a low of 89% for precision, and a high of 95% for recall. For all the No Fraud cases, the model correctly identified 89%. For Class 1 (Fraud) we have a low of 88% for recall, and a high of 94% for precision. For all the Fraud cases, the model correctly identified 94%. The AUC score of 96% is the Area Under the Curve, which tells us that the model's ability to discriminate between Fraud and No Fraud classes is very strong. After the logistic regression, we can see that the train and test  accuracy is 91%, which is fairly good.
To further the accuracy, we can perform a XGBoost Classifier, where the parameters tell us the number of trees, step size shrinkage, maximum depth of each tree, minimum sum of instance weight in a leaf, the fraction of samples used to train each tree, the fraction of features used when building each tree, the minimum loss reduction, the L1 regularization term on weights, and the L2 regularization term on weights. This classifier is an algorithm used to optimize performance in classification tasks. This further increased our performance metrics for Class 0 (No Fraud) with 94%, 97%, and 95% for precision, recall, and F1-score. For Class 1 (Fraud) with 97%, 94%, and 95%. The accuracy is now 95%. Finally, our test and training sets have an accuracy of 95% which is higher than out previous 91%. This indicates that our model is performing well and predicts 95% of the data. We can now visualize a Decision Tree which has several layers to it. 
![ClassificationReport](https://github.com/user-attachments/assets/d1ad6a76-100a-4126-b6fd-6627582fc38c)
![Decision Tree](https://github.com/user-attachments/assets/75fbe343-35e8-4f2f-9e1d-4e5fd85da43d)

One major challenge I encountered was the model selection and imbalance in the data. I had to figure out how to use SMOTE within my models to keep it balanced at 50/50. I also struggled with choosing which models were best suited for my data. There are several models that can be used with classification tasks, so I chose a couple to compare the accuracy and results. Overall I found the XGBoost Classifier to be the best. I had to get some help from AI and from other similar projects to help with this classifier as I did not know what the parameters meant. It is an implementation of gradient-boosting decision trees optimized for efficiency and performance. But afterwards, we can see that my accuracy boosted to 95% and the performance metrics were high, indicating that this model was performing well. Overall, since the original data had so many transactions, it was harderto correctly fit my model so everything performed well. Also, since my features are hidden due to confidentiality, we cannot know what features effected if the transaction was identified as Fraud or No Fraud. Some future work I could do would include unsupervised learning like using K-Menas to identify more patterns in the data or implement time series models to simulate real time fraud detecttion scenarios. 
