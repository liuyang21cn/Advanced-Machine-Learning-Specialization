# Week2
### Visualization tools
	Seaborn
	Plotly
	Bokeh
	ggplot
	Graph visualization with NetworkX
### Others
[Biclustering algorithms for sorting corrplots](http://scikit-learn.org/stable/auto_examples/bicluster/plot_spectral_biclustering.html)

Question 1
Select true statements
Correct answers:

We use validation to estimate the quality of our model. Correct! This is the main purpose of validation.
The logic behind validation split should mimic the logic behind train-test split. Correct! This is the main rule of making a reliable validation.
Underfitting refers to not capturing enough patterns in the data. Correct! Because a model cant utilize all existing patterns, it has lower quality than it could have.
Incorrect answers:

The model, that performs best on the validation set is guaranteed to be the best on the test set. Incorrect. Target in the test set can have different distribution and our score estimation can fail.
Performance increase on a fixed cross-validation split guaranties performance increase on any cross-validation split. Incorrect. You can overfit to the specific CV-split. You should change your split from time to time to reduce the chance of overfitting.
Question 2
Usually on Kaggle it is allowed to select two final submissions, which will be checked against the private LB and contribute to the competitor's final position. A common practice is to select one submission with a best validation score, and another submission which scored best on Public LB. What is the logic behind this choice?
Correct answers:

Generally, this approach is based on the assumption that the test data may have a different target distribution compared to the train data. If that would be the true, the submission which was chosen based on Public LB, will perform better. If, otherwise, the above distributions will be similar, the submission which was chosen based on validation scores, will perform better.
Incorrect answers:

Generally, this approach is based on the assumption that people rarely tend to overfit to the Public LB. Almost always you have a lot of data in the test set and it is quite hard to overfit. Indeed, this render validation useless.
Generally, this approach is based on the assumption that validation is rarely valid in competitions. Almost always it is hard to trust your validation and thus you should account for both cases if the validation will succeed and if the validation will fail.
Question 3
Suppose we have a competition where we are given a dataset of marketing campaigns. Each campaign runs for a few weeks and for each day in campaign we have a target - number of new customers involved. Thus the row in a dataset looks like:
Campaign_id, Date, {some features}, Number_of_new_customers
Test set consists of multiple campaigns. For each of them we are given several first days in train data. For example, if a campaign runs for two weeks, we could have three first days in train set, and all next days will be present in the test set.
Identify train/test split in a competition.
Correct answer:

Combined split. For each campaign train and test are divided by a date, and this date can be different for different campaigns. Thus, split is made by id and by time.
Incorrect answers:

Random split
Time-based split
Id-based split
Question 4
Which of the following problems you usually can identify without the Leaderboard?
Correct answers:

Different scores/optimal parameters between folds. Correct. This can be identified during validation.
Public leaderboard score will be unreliable because of too little data. Correct. Usually you can estimate variance of Public LB score using validation. You need to train a model and see how its score varies on different folds with the same size as Public LB.
Train and test data are from different distributions. Correct! Often enough we can find out this during EDA. To refresh your memory about this problem, review the last video in the Validation module.
Incorrect answers:

Train and test target distribution are from different distributions. Incorrect! To do this, we would need to have test target values, which is not possible in a competition.

[Validation in Sklearn](http://scikit-learn.org/stable/modules/cross_validation.html)
[Advices on validation in a competition](http://www.chioka.in/how-to-select-your-final-models-in-a-kaggle-competitio/)

Question 1
Suppose that you have a credit scoring task, where you have to create a ML model that approximates expert evaluation of an individual's creditworthiness. Which of the following can potentially be a data leakage? Select all that apply.
Correct answers:

An ID of a data point (row) in the train set correlates with target variable. Data was not shuffled, this information can not be used in real-world scenario.
First half of the data points in the train set has a score of 0, while the second half has scores > 0. Same as above, data was not shuffled, this information can not be used in real-world scenario..
Incorrect answers:

Among the features you have a company_id, an identifier of a company where this person works. It turns out that this feature is very important and adding it to the model significantly improves your score. This is a perfectly fine categorical feature, don't mix it up with and ID of a data point.
Question 2
What is the most foolproof way to set up a time series competition?
Correct answers:

Split train, public and private parts of data by time. Remove all features except IDs (e.g. timestamp) from test set so that participants will generate all the features based on past and join them themselves. Correct! Only complete removal of all features from test set can guarantee that there is no data leakage.
Incorrect answers:

Make a time based split for train_test and a random split for public_private. Vulnerable to leaderboard probing.
Split train, public and private parts of data by time. Remove time variable from test set, keep the features. Participants can try to reverse engineer time order and exploit future peeking.
Question 3
Suppose that you have a binary classification task being evaluated by logloss metric. You know that there are 10000 rows in public chunk of test set and that constant 0.3 prediction gives the public score of 1.01. Mean of target variable in train is 0.44. What is the mean of target variable in public part of test data (up to 4 decimal places)?
Correct answers:

~0.771 Use logloss formula.
Question 4
Suppose that you are solving image classification task. What is the label of this picture?
Correct answer is 3. Check image name!

## Additional material and links
[Perfect score script by Oleg Trott](https://www.kaggle.com/olegtrott/the-perfect-score-script) — used to probe leaderboard
[Page about data leakages on Kaggle](https://www.kaggle.com/wiki/Leakage)

