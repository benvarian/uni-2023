## multiple linear regression 
- instead of fitting a seperate simple linear regression model for each predictor, a better approach is to extend the simple linear regression model so that it can directly accommodate multiple predictors 
- **do this by giving each predictor a seperate slot coefficient in a single model.**
- in the advertising example, the model becomes 
	- ![[Screenshot 2023-04-15 at 1.28.05 pm.png]]

## estimating the regression coefficients 
- ![[Screenshot 2023-04-15 at 1.30.36 pm.png]]
- ![[Screenshot 2023-04-15 at 1.51.38 pm.png]]
	- ![[Screenshot 2023-04-15 at 1.51.59 pm.png]]
	- this dispalys the multiple regression coefficient estimates when TV, radio and newspaper advertising budgets are used to predict product sales using the advertising data 
	- the fitted line is given by 
		- $\widehat{sales}$ = 2.9389 + 0.0458 x TV + 0.1885 x radio - 0.0010 x newspaper
		- interpret these results as 
			- for a given amount of TV and newspaper advertising, spending an additional $1,000 on radio advertising leads to an increase in sales by approximeately 189 units 

## some important questions 
- when we perform multiple linear regression, we usually are interested in answering a few important questions 
	- is at least one of the predictors X1, X2, ... , Xp useful in predicting the response 
	- do all the predictors help to explain Y, or is only a subset of the predictors useful 
	- how well does the model fit the data 
	- given a set of predictor values, what response value should we predict, and how accurate is our prediction

### one: is there a relationship between the response and predictors 
- the F-statistic for the multiple linear regression model obtained by regressing sales onto radio, TV and newspaper 
	- ```summary(lm(sales~TV+radio+newspaper,data=Advertising))```
		- ![[Screenshot 2023-04-15 at 2.05.10 pm.png]]
		- here the F-stat is 570, since it is far greater than 1 it provides compelling evidence against the null hypothesis $H_0$ 
		- **in other words, the large F-statistic suggests that at least one of the advertising media must be related to sales**
		- the p-value associated with the f-statistic is essentially zero, **so we have extremely strong evidence that at least one of the media is associated with increased sales**
			- can compute the p-value as 
			- 1-pf(570.3,3,196)
	- we may be interested in testing the significance of both radio and newspaper from the full model that includes radio, newspaper and TV:
		- ![[Screenshot 2023-04-15 at 2.09.51 pm.png]]
		- ![[Screenshot 2023-04-15 at 2.11.29 pm.png]]
		- ![[Screenshot 2023-04-15 at 2.11.39 pm.png]]
		- ![[Screenshot 2023-04-15 at 2.34.22 pm.png]]
		- ![[Screenshot 2023-04-15 at 2.34.07 pm.png]]
		- these provide infomration about whether each individual predictor is related to the response
		- ![[Screenshot 2023-04-15 at 2.35.23 pm.png]]
		- **so it reports the partial effect of adding that variable to the model.** these p-values indicate that TV and raadio are related to sales, but there is no evidence that newspaper is associated with sales 
- the approach of using a F-statistic to test for any association between the predictors and the response works when p is relatively small, and certainly small compared to n.
- If p > n then there are more coefficients $β_j$ to estimate than observations from which to estimate them. In this case we cannot even fit the multiple linear regression model using least squares, so the F-statistic cannot be used, and neither can most of the other concepts that we have seen so far in this chapter. **When p is large, some of the approaches discussed in the next section, such as forward selection, can be used.**

### two: deciding on important variables 
- if we conclude on the basis of that p-value that at least one of the predictors is related to the response, then it is natural to wonder which are the guilty ones.
- **forward selection**
	- beging with null model-a model that contains an intercept but no predictors 
	- then fit p simple linear regressions and add to the null model the variable that results in the lowest RSS.
	- then add to that model the variable that results in the lowest RSS for the new two-variable model 
	- continued until some stopping rule is satisfied 
- **backward selection**
	- start with all variables in the model, backward remove the variable with the largest p-value, the value that is least statistically significant 
	- the new (p-1) variable model is fit, and the variable with the largest p-value is removed 
	- continues until a stopping rule is reached 
	- may stop when all remaning values have a p-value below some threshold 
	- cannot be used if p > n
- **mixed selection**
	- start with no variables in the model
	- add the variable that provides the best fit 
	- continue to add varaibles one-by-one 
	- if at any point the p-value for one of the variables in the model rises above a certain threshhold, we then remove that variable from the model
	- we continue to perform these forward and backward steps until all variables in the model have a sufficiently low p-value 


## three: model fit 
- the model containing only TV as a predictor had an $R^2$ of 0.6119
- adding radio to this model leads to a substantial improvement in $R^2$ -> 0.8972
- this implies that a model that uses TV and radio expenditures to predict sales is substantially better than one that uses only TV advertising. 
- the mode lthat contains TV and radio as predictors has an RSE of 1.681
- add newspaper in and its 1.686 
- in contrast, the model that contains only TV has an RSE of 3.259
- this collaborates our previous conclusion that a model that uses TV and radio expenditures to predict sales is much more accurate than one that only uses TV spending 
- furthermore, given that TV and radio expenditures are used as predictors, there is no point in also usiing newspaper spending as a predictor in the model