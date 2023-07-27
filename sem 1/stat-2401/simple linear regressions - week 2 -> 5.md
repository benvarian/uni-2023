## analysiing advertising data 
- is there a relationship between advertising and sales 
- how strong is the relationship between advertising budget and sales 
- which meida contribute to sales 
- how accurately can we estimate the effect of each medium on sales 
- how accurately can we predict future sales 
- is the relationship linear?
- is there synergy among the advertising media 


## simple linear regression
- straightforward approach for predicting a quantitive response Y on the basis of a single predictor variable X
- ![[Screenshot 2023-04-15 at 11.30.08 am.png]]


## estimating the coefficients 
- ![[Screenshot 2023-04-15 at 11.33.51 am.png]]
- ![[Screenshot 2023-04-15 at 11.36.29 am.png]]
	- can interpret this as, an additional $1000 spent on TV advertising is associated with selling aproximately 47.5 additional units of the product 

## assessing the accuracy of the coefficient estimates 
- ![[Screenshot 2023-04-15 at 11.43.12 am.png]]
	-  ![[Screenshot 2023-04-15 at 11.43.52 am.png]]
- ![[Screenshot 2023-04-15 at 11.45.16 am.png]]
	- how to analyse in refernce to tv data 
		- can conclude that in absence of any advertising, sales will on average fall somewhere between 6,130 and 7,940 units. Futhermore, for each $1000 increase in television advertising, there will be an average increase in sales of between 42 and 53 units 
- ![[Screenshot 2023-04-15 at 11.48.34 am.png]]
	- ![[Screenshot 2023-04-15 at 11.48.45 am.png]]

- hypothesis tests on the coefficients 
	- most common test involves testing teh null test hypothesis of 
		- $H_0$: there is no relationship between X and Y 
	- vs the alternative hypothesis 
		- $H_1$ there is some relationship between X and Y 
	- mathmatically this equates to 
		- H0 : B1 = 0 
		- vs
		- H1: B1 ≠ 0
	- since if B1 = 0, then the model Y = B0 + B1 X + e, reduces to Y = B0 + e and X is not assocaited with Y
- ![[Screenshot 2023-04-15 at 11.48.34 am.png]]
	- so we have 
		- ![[Screenshot 2023-04-15 at 11.53.40 am.png]]
	- the probabilities of seeing such values if H0 is true are virtually zero, hence we can conclude that B0 ≠ 0 and B1 ≠ 0.

- once we have rejected the null hyptothesis H0 in favour of H1, we want to quantify the extent to which the model fits the data, the quality of a linear regression fit is typically assessed using two related quantitie, the **residual standard error (RSE)** and the $R^2$ statistic
	- ![[Screenshot 2023-04-15 at 11.59.35 am.png]]
	- ![[Screenshot 2023-04-15 at 11.59.45 am.png]]
	- the RSE is 3.259. actual sales in each market deviate from the true regression line by approximately 3,259 units on average
	- the mean values of sales over all markets is approximately 14,000 units, and so the percentage error is 3,259/14,000 = 23%

## prediction for the simple linear regression 
- ![[Screenshot 2023-04-15 at 12.02.51 pm.png]]
	- we can interpret this to mean that 95% of intervals of this form will contain the true value of f(X) = b0 + b1X
- ![[Screenshot 2023-04-15 at 12.04.05 pm.png]]
	- means that 95% of intervals of this form will contain the true value of Y for this city. 
- now illustrate the data 
	- ![[Screenshot 2023-04-15 at 12.06.19 pm.png]]

## analysis of variance 
- there is a linear association between Y and X if 
	- y = b0 + b1x + e
- and b1 ≠ 0. 
- if we knew that b1 ≠ 0 then we would predict Y by 
	- ![[Screenshot 2023-04-15 at 12.09.59 pm.png]]
- otherwise, if we knew that B1 = 0 then we can predict Y by 
	- $\hat{y}$ = $\overline{y}$ 
- ![[Screenshot 2023-04-15 at 12.12.30 pm.png]]
- F-statistic = 312.14 = $17.67^2$ 

## $R^2$ statistic
- the Residual standard error (RSE) provides an absolute measure of lack of fit of the model Y = b0 + b1X + e to the data. 
- the $R^2$ statistic provides an alternative measure of fit. it takes the form of a proportion, the proportion of variance explained, and so it always takes on a value between 0 and 1, and is independent of the scale of Y
- ![[Screenshot 2023-04-15 at 12.16.17 pm.png]]
- the total sum of squares (TSS)
	- measures the total variance in the reponse Y
- the residual sum of squares (RSS)
	- measures the amount of variability that is left unexplained after performing the regression 
- then TSS-RSS measures the amount of variability in the response that is explained by performing the regression, and $R^2$ measures the proportion of variability in Y that can be exaplined using X 
- an $R^2$ statistic that is close to 1 indicates that a large proportion of the variability in the response has been explained by the regression. number near 0 indicates that the regression did not explain much of the variability in the response 
- ![[Screenshot 2023-04-15 at 12.20.21 pm.png]]
	- the $R^2$ was 0.6119, and so just under two-thirds of the variability in sales is explained by a linear regression on TV
- example
	- fitted model 
		- ![[Screenshot 2023-04-15 at 12.22.52 pm.png]]
	- ![[Screenshot 2023-04-15 at 12.23.01 pm.png]]
	- ![[Screenshot 2023-04-15 at 12.23.09 pm.png]]
		- as cholesterol increases by 1, mean BMI is estimated to increase by 0.168 and 0.649