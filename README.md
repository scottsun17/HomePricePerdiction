# HomePricePredictions
## Introduction
What is a home value? How much does a home worth? How can I sell my home to a higher price? Those are the questions many home sellers ask. The problem asked here is:<br /><br /><b> What are the driving factors that affect the price of a home?</b><br />
Further more, <b>How can we increase the sale price of a home?</b>


## DataSet
For this project, we use dataset from Kaggle: <a href="https://www.kaggle.com/c/house-prices-advanced-regression-techniques/data">House Prices</a><br />
The data set contains housing data from Idaho, such as square footage, number of bedrooms, above ground living space, and number of garages. <br />
For more data description, please view <a href="https://github.com/scottsun17/HomePricePrediction/blob/master/Data/data_description.txt">here</a>

## Methods
### Step 1: Dividing Dataset
The dataset is divided into three sets: Top, Average, and Bottom neighborhood.
The division criteria is based on the average price of each neighborhood.![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/Neighborhoods.PNG)It is divided into top three neighborhoods, bottom three neighborhoods, and the rest as average neighborhoods. <br>
**Top Three Neighborhoods**: NoRidge, NridgHt, StoneBr  
**Bottom Three Neighborhoods**: MeadowV, IDOTRR, BrDale

### Step 2: Build Prediction Model Based on Correlation
In this step, we identify the factors in the dataset that have strong correlation with Home 'SalePrice' for each Neighborhoods Division.
<br />
For Top Three Neighborhoods, we see the following high correlation coefficient factors:
![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/TopNeighborhoodsCorrelations.PNG)

For Bottom Three Neighborhoods, we see the following high correlation coefficient factors:
![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/BotNeighborhoodsCorrelations.PNG)

### Step 3: Build Prediction Models with Random Forest Regressor 
In this step, we use the three dataset to build three models using its own top correlation coefficient factors.

### Step 4: Predict the Price of the Same House using Different Models
We use the three models from step 3 to predict the price of the same house and comparing its predicted price. We receive the following results:
|Neighborhood|Sale Price|
|--|--|
| Top | 230099.49 |
| Average | 117948.23 |
| Bot | 105282.87 |

![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/SameHoursePriceBasedonLocation.PNG)
The same house in different neighborhoods can be sold at different prices. 

### Step 4: Further Analysis to Identify Price Increase Home Improvement Factors
In this step, we tested out to certain home improvement's effects on Home Price. 
We used the same home from step 3, assume it is located in the top three neighborhoods and improved it top three correlation factors. We received the following results: <br />
<b>Test 1:</b> Increase GrLivArea by 100% and perdict the price
[https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/Test1Result.PNG](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/Test1Result.PNG)
The price of the home has <b>decreased</b> by 2724.92
<br />
<b>Test 2:</b> Increase OverallQual by 2 points
![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/Test2Result.PNG)
The price of the home has <b>increased</b> by 20480.97
<br />
<b>Test 3:</b> Increase TotRmsAbvGrd by 2 rooms
![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/Test3Result.PNG)
The price of the home has <b>increased</b>by 3169.91

### Step 5: Finding Contradiction in Results
Based on assumption, we assume that improvement in the house will also improve home price. However, improvement in GrLivArea has yield a negative effect even though it has the strongest correlation with sale price. Thus we need to further analyze weather GrLivArea is the most related factor in predicting sale price.  

Here we use Extra Tree Regressor to assess <b>features importances</b>
![enter image description here](https://raw.githubusercontent.com/scottsun17/HomePricePrediction/master/Picture/FeatureImportance.PNG)
We identify that GarageCars has the highest feature importance in home price prediction even though it was not one of the top correlation factors. 
Home improvement around GarageCars will yield better return than other home improvements 

 ## Conclusion and Possible Model Improvements
 Based on the above Models and Testings, we are fairly confident in predicting the price of a home and determine what home improvements to do, in order to receive the better sale price. The location of the home has a significant effect on the price of the home. Same/similar home located in different neighborhoods may vary the price of the home by significant amount. Different neighborhoods also value certain home features more than the others. Thus, we came up with the following possible improvement for the model:
 

 1. Build models for each individual neighborhood rather than aggregate certain neighborhood together.
 2.  Replying on Feature Importance model result as factors in prediction model rather than simply top correlation coefficient factors.
