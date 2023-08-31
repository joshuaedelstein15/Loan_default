#### 07/30/23

#### Joshua Edelstein

# Loan Default

## Overview
Primary revenue generation for banks heavily relies on the dispersion of loans, with the pivotal factor being the successful repayment of these loans. The assurance of loan repayment plays a critical role in enhancing their revenue streams. However, the default rate has exhibited a concerning upward trend. It has become imperative for banks to retain the capacity to extend loans while maintaining the confidence that a substantial proportion will be promptly repaid.

Recent developments underscore the gravity of the situation. Notably, in the month of June alone, four corporate entities filed for bankruptcy. This series of events pushed the cumulative default volume for the preceding 12 months to a staggering $24 billion, marking the highest figure recorded since April 2021. These occurrences shed light on the growing challenges banks face in maintaining the delicate equilibrium between extending credit and safeguarding their financial stability.


## Business Understanding
The American Bankers Association has come to us to try fix the issue of the rising default rates. Although many banks have a strong customer base and are constantly offering loans, their clients are defaulting on loans at a much higher rate than they would have liked. We are tasked we figuring out possible problems and solutions with the current lending process. 

In this scenario we will break the data into 2 categories: a) the columns used to predict default. b) the default column itself, which will be structured in the positive. Meaning that a 1 in that column will mean that it was paid back.

It is important to take into account whether the affects of a false positive vs false negative is worse. In this case we are predicting whether a loan will be paid back. Therefore a false positive means we predict a loan will be paid back, when in reality it won't be, this is seen by precision. A false negative is when we predict a customer won't pay a loan back, when in reality they do pay it back, this is seen by recall. In this case it slightly depends on what the bank is looking for, but since our bank has a steady flow of clients, we don't need to be concerned about turning customers away from loans. As such precision is far more important here, as the result of a false positive is losing out on the principle of the whole loan. While a false negative means that we wont offer a loan, and thus won't gain the extra interest over the course of a few years. As such we will attempt to tune our model to more heavily focus on precision.


<div>
<img src="Images/inside_bank1.jpg", width = 800, height = 400/>
</div>

## Data Understanding

The public data set was provided by the SBA(Small Business Association) and can be downloaded from kaggle. The years the loans were approved range from 1969 to 2014. However, the range of the loans due date was from 1973 until 2035. We see that we are dealing with many loans that are not even due yet.

Data Source: https://www.kaggle.com/datasets/mirbektoktogaraev/should-this-loan-be-approved-or-denied

We began by performing EDA on our data.

The first thing we looked at is where in the USA the data came from. We had to merge our data that contained zipcodes with a different dataframe that contained longitude and latitude. At first we plotted our longitude and latitudes on a blank background. Being that there were so many datapoints, it created a pretty good map of the USA. 

<div>
<img src="Images/map1.jpg", width = 400, height = 300/>
</div>

We then moved on to create a fancier map that Folium and clustering. This map was interactive and created clusters of data points depending on how much you zoomed in or out

<div>
<img src="Images/map2.jpg", width = 400, height = 300/>
</div>

Finally, we pulled up a bar graph of the breakdown of our target column, whether the loan was paid back or not. 

<div>
<img src="Images/default_rate.jpg", width = 400, height = 300/>
</div>

The breakdown of the loans was that 76.6% were paid back and 23.4% defaulted. As such we see that we are dealing with a slightly imbalanced dataset. We then moved on to our data preparation stage.

## Data Preparation

Being that we were dealing with a very messy dataset, there was a lot of cleaning that needed to be done. To prevent data leakage we did a `train_test_split` before any of the cleaning. The cleaning was composed of dropping rows, dropping columns, creating dummy columns, stripping string data and reformating, and making sure everything was stored as the right datatype. I will now highlight three major steps in the cleaning process. 

One of the columns in our dataset contained the bank that offered the loan. This is very useful information; however, there were over 5000 value counts, making the data unusable in its current format. We needed to figure out a way to group the data so that there was a reasonable amount of value counts, allowing us to create dummy columns. In the end, we decided to rename all the values based on a dictionary depending on the size of the chain. In the end we only had six different values ranging from `Bank_huge` to `Bank_tiny`.

The next column we needed to fill was a boolean column indicating whether the business was in a urban area or rural area. This column had over 200,000 missing values. To fill this column we found the urban rural codes for all zipcodes in the USA, and merged this on to our dataframe, to fill almost all the missing values.

The last column we needed to fill, was another boolean column which indicated whether the business had a revolving line of credit. This column contained over 100,000 missing values, and there was no clearn way how to fill them. We did some EDA on the column and discovered that although the column in general had more 0s than 1s. In the years that there were missing values the columns actually contained more 1s than 0s. We then created four theoretical ways to clean the data, the first was to drop all the rows with missing data, the second was drop the column, the third was to fill all the missing values with 1s, and the last was to create a dummy column for 0,1 and missing. We then ran a very basic Decision Tree Classifier on them to determine which way performed the best. In the end the dummy columns performed the best, as such we set it inplace and moved on to our modeling

