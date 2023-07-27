
## equation of a line 
- the equation of a line is 
	- y = mx + c
- where m is the slope or gradient 
- c is the y intercept 

## plotting of lines 
- ![[Screenshot 2023-03-15 at 10.41.31 am.png]]

## residuals
- the difference between predicted values of y and observed values of y
- ![[Screenshot 2023-03-15 at 10.41.42 am.png]]


## method of least squares 
- the best line would be the one where 
	- the sum of the squares of the residuals 
- is as small as possible 
- pos or neg devations count equally 
- large deviations count signifficantly more 

## notation 
- ![[Screenshot 2023-03-15 at 10.43.43 am.png]]

## line of best fit 
- so the best linear equation fitting the fater / son data is 
	- y = 86.088 + 0.514x
- so the best guess for height of the son of a 180cm father would be 
	- 86.088 + 0.514 x 180 = 178.76

## best line 
- ![[Screenshot 2023-03-15 at 10.46.55 am.png]]

## the anscombe quartet 
- a famour collection of four datasets, each containing elevent (x,y) pairs 
- each of the datasets has almost the same summary data 
- each of the datasets has the same linear model 

### anscombe quartet scatterplots 
- ![[Screenshot 2023-03-15 at 10.48.20 am.png]]

#### anscombe regression lines 
- ![[Screenshot 2023-03-15 at 10.48.42 am.png]]

## terminology 
- the x-varaible is called the predictor, or explanatory variable 
- the y-varaible is called the response variable 
- the line is called the fitted line and expressed in the form 
	- $\hat{y} = b_0 + b_1x$ 
- the hat notation, such as y above, is used to denote a estimated or predicted value derviced from a model 

## are residuals errors 
- for each data point ($x_i$, $y_i$ ) we have 
	- $\hat{y} i = b_0 + b_1x_1$ 
- which is the predicted value for $y_i$ 
- so put 
	- $e_i = y_i - \hat{y}_i$ 
- and call this the residual or error 
- its the difference between the observed value and the fitted value 

### residual plot 
- where vertical axis is the residuals, and whose horizontal axis is the predictor varaible or the fitted value 
- ![[Screenshot 2023-03-15 at 10.57.04 am.png]]

#### satisfactory residual analysis 
- ![[Screenshot 2023-03-15 at 10.57.38 am.png]]

#### unsatisfactory residual analysis 
- ![[Screenshot 2023-03-15 at 10.57.59 am.png]]

#### more residual analysis 
- ![[Screenshot 2023-03-15 at 10.59.23 am.png]]