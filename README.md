# Ames, IA Housing Price Predictions

### Executive Summary

For this project, the current year will be set to 2011. This is a time right after the financial crisis where home prices are starting to bounce back. Homeowners are interested in selling their homes and they are turning to the internet before putting their homes on the market. They want to gauge how to price their homes and have questions about specific house features and home value. 

A common google search that has spiked in popularity recently is “does the kitchen sell the house?” According to sites like Fales Realty, the kitchen kitchen is one of the most important rooms when selling a house. ([source](http://www.falesrealty.com/BLOG/ArticleID/1/Real-Estate-Secrets-Why-and-How-Kitchens-Sell-Homes)) 

A real estate company in Ames, IA noticed this phenomenon in search activity and hired me to research this question more in depth for their community. In my analysis, I will use a regression model to predict housing prices based on home features and use this to determine if kitchen quality adds value to a home. I will be presenting my results to the real estate company that hired me. 

---

### Datasets

There 4 datasets included in the [`datasets`](./datasets/) folder were used for this project and described below. 

* [`test.csv`](./datasets/test.csv): Test data to pull in for Kaggle submission
* [`train.csv`](./datasets/train.csv): Training data to fit regression models
* [`sample_sub_reg.csv`](./datasets/sample_sub_reg.csv): Baseline submission for Kaggle competition
* [`submissionRF`](./datasets/submissionRF): Kaggle competition submission

---

### Data Dictionary

The data dictionary can be found on Kaggle [Kaggle](https://www.kaggle.com/c/dsi-ames/data).

The data descriptions can be found here [data description](http://jse.amstat.org/v19n3/decock/DataDocumentation.txt).

---

### Methodology 

The dataset used for this analysis is 2006 – 2010 Ames, IA home prices with about 2,000 entries and over 70 columns of different housing features. The data was cleaned to prepare for modeling. Outliers were removed, features were transformed appropriately for ordinal data, categorical variables were one hot encoded, and nulls were accounted for.

Feature extraction and feature interaction was performed on cleaned data. I extracted features such as the age of the house in 2011, the remodel age of the house in 2011, and total number of bathrooms in the house. I also added feature interactions between variables such as quality and condition for various features of the house (overall, basement, garage), age and remodel age, the log of the ages, total rooms with total bathrooms, and kitchen quality and number of kitchens to see what their interaction was together and if this added more explanation to the model. 

I performed EDA using correlation maxtrices, heat maps, and scatter plots to explore relationships in x variables with each other and with y variable (sales price).

Linear Regression, Ridge Regression, and Lasso Regression were used to evaluate best prediction method for home prices based on home features. I also focused on the kitchen quality coefficient and how this is interpreted in terms of the best model to answer research question.

To evaluate which regression model is the best for predicting home prices, various combinations of features and regression methods will be tested to find the best one based on the criteria below:
 - Does the model meet the LINEI assumptions?
 - How does the model’s RMSE compare to the baseline model and other models?
 - How do the R2 scores for training, cross validation training mean, and testing groups compare to each other and other models?
 - Is the model’s coefficients easily interpretable and statistically significant (< 0.05 p value)?
 - Does kitchen quality turn out to be a significant feature in the model?

---

### Conculsions

7 different regression models were evaluated in this study. I iterated through models starting with a kitchen sink linear regression, then adding and subtracting features, and lastly adding in regularization techniques. I selected my best model, also shown as the production model, because it met the evaluation criteria the best. 

The production model ended up with 33 significant features (mix of regular features and a couple feature-engineered features.) The features covered house age, quality, number of rooms/bathrooms, building type, and neighborhood. Most of the variables had a linear relationship with price. The plot of the errors showed that they are independent, normally distributed, and have equal variance, especially compared to some of the other models I looked at. There is only high correlation between a handful of variables. The RMSE for the production model had a RMSE of $24,188 which was lower than the other models and also lower compared to the baseline RMSE of $71,469. The r2 scores for my training and testing groups were around 0.88, meaning that these models are accounting for 88% of the variance in the dataset and it's a pretty strong model. Since the r2 scores were very high and close together this tells me that the model performs well on seen and unseen data, and it performs better/more consistently compared to other models. The coefficients in this model are statistically significant and it shows that kitchen quality is a significant feature to predict home prices. The drawbacks of this model are slight multicollinearity and some features do not have a perfect linear relationship with price.

The production model’s coefficients and the corresponding p values can be used to infer the effect of home features on the selling price. 
The features that have the largest impact on the selling price in terms of this model are overall quality, the age of house and/or remodel, exterior quality, kitchen quality, basement exposure, functionality, total rooms, total bathrooms, proximity conditions, building types, and neighborhoods. 

Going back to the question of "Does the kitchen sell the home?" - A home’s price is determined by many different features as shown in this model, but yes, we can see that kitchen quality is one of the significant features that contributes to the home price. As the kitchen quality rating increases, price increases. According to our model holding all else equal, for every increase in the kitchen quality rating (1 – 5), the selling price will increase by $8,053.50 on average. 


### Recommendations

According to the dataset, about 90% of homes sold in Ames, IA did not have a 5 star kitchen quality rating. Knowing the potential increase in home price by increasing the kitchen quality rating is valuable information to all the homeowners with a less than excellent kitchen quality rating. The real estate company should capitalize on the success of the strong model produced from this study. The company can now confidently advise their clients that increasing kitchen quality has a positive impact on home price and have an idea of what that impact is in dollars. The real estate company could also consider making the results of this study available for purchase to profit from this study. 
