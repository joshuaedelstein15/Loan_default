#### 07/30/23

#### Joshua Edelstein

# Loan Default

## Overview
Primary revenue generation for banks heavily relies on the dispersion of loans, with the pivotal factor being the successful repayment of these loans. The assurance of loan repayment plays a critical role in enhancing their revenue streams. However, the default rate has exhibited a concerning upward trend, vacillating within the range of 1% to 2%. It has become imperative for banks to retain the capacity to extend loans while maintaining the confidence that a substantial proportion will be promptly repaid.

Recent developments underscore the gravity of the situation. Notably, in the month of June alone, four corporate entities filed for bankruptcy. This series of events pushed the cumulative default volume for the preceding 12 months to a staggering $24 billion, marking the highest figure recorded since April 2021. These occurrences shed light on the growing challenges banks face in maintaining the delicate equilibrium between extending credit and safeguarding their financial stability.


## Business Understanding
A smaller end bank, named EconoTrust bank, has come to us and expressed their struggle with defaulting loans. Although they have a strong customer base and are constantly offering loans, their clients are defaulting on loans at a much higher rate than they would have liked. 

In this scenario we will break the data into 2 categories: a) the columns used to predict default. b) the default column itself, which will be structured in the positive. Meaning that a 1 in that column will mean that it was paid back.

It is important to take into account whether the affects of a false positive vs false negative is worse. In this case we are predicting whether a loan will be paid back. Therefore a false positive means we predict a loan will be paid back, when in reality it won't be, this is seen by precision. A false negative is when we predict a customer won't pay a loan back, when in reality they do pay it back, this is seen by recall. In this case it slightly depends on what the bank is looking for, but since our bank has a steady flow of clients, we don't need to be concerned about turning customers away from loans. As such precision is far more important here, as the result of a false positive is losing out on the principle of the whole loan. While a false negative means that we wont offer a loan, and thus won't gain the extra interest over the course of a few years. As such we will attempt to tune our model to more heavily focus on precision.


<div>
<img src="Images/inside_bank1.jpg", width = 800, height = 400/>
</div>

## Data Understanding

The public data set was provided by the SBA(Small Business Association) and can be downloaded from kaggle. The years the loans were approved range from 1969 to 2014. However, the range of the loans due date was from 1973 until 2035. We see that we are dealing with many loans that are not even due yet.

Data Source: https://www.kaggle.com/datasets/mirbektoktogaraev/should-this-loan-be-approved-or-denied

We began by performing EDA on our data.

See screenshots

## Data Preparation


