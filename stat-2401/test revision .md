t-stat 
f-stat
estimator in matrix form 
p-value
manually figure out confidence intervals
basic rules 


## residual sum of squares formula 
- ![[Screenshot 2023-05-12 at 12.26.52 pm.png]]

## least squares coefficient estimates 
- ![[Screenshot 2023-05-12 at 12.37.13 pm.png]]

## standard errors for b0 and b1
- ![[Screenshot 2023-05-12 at 12.37.40 pm.png]]

## variance for b0 and b1
- ![[Screenshot 2023-05-12 at 12.38.08 pm.png]]

## residual standard error (RSE)
- ![[Screenshot 2023-05-12 at 12.39.17 pm.png]]
- writes like $\widehat{SE} (\widehat{B_1})$  
- ![[Screenshot 2023-05-12 at 12.40.33 pm.png]]

## confidence intervals 
- for b1
	- ![[Screenshot 2023-05-12 at 12.42.22 pm.png]]
- b0 
	- ![[Screenshot 2023-05-12 at 12.42.48 pm.png]]

## more stuff
- ![[Screenshot 2023-05-12 at 12.44.44 pm.png]]
- ![[Screenshot 2023-05-12 at 12.44.56 pm.png]]

## testing hypothesis 
- ![[Screenshot 2023-05-12 at 1.20.03 pm.png]]
- ![[Screenshot 2023-05-12 at 1.20.41 pm.png]]
- if there is no relationship between X and Y, then we expect that the t-statistic will have a t-distribution with n-2 degrees of freedom

## p-value 
- if we see a small p-value, then we can infer that there is an assocaition between the predictor and the response. We then reject the null hypthesis, meaning we declare that there is a relationship that exists between X and Y, if the p-value is small enough 


## residual standard error (RSE) and the $R^2$ 
- ![[Screenshot 2023-05-12 at 1.25.08 pm.png]]
- the residual standard error is an estimate of the standard deviation of the resisuals.
- the RSE is the average amount that the respone will deviate from the true regression line.
- considered a measure of the lack of fit of the model to the data
	- ![[Screenshot 2023-05-12 at 1.26.27 pm.png]]
	- ![[Screenshot 2023-05-12 at 1.26.41 pm.png]]


## analysis of variance 
- ![[Screenshot 2023-05-12 at 1.33.24 pm.png]]
- TSS = total sample variability 
- RSS = unexplained variability 
- RegSS = variability explained by the model 
- analysis of variance table 
	- ![[Screenshot 2023-05-12 at 1.35.15 pm.png]]
- ![[Screenshot 2023-05-12 at 1.35.46 pm.png]]

## $R^2$ stat
- ![[Screenshot 2023-05-12 at 1.36.24 pm.png]]
- ![[Screenshot 2023-05-12 at 1.39.46 pm.png]]

## estimating regression coefficients 
- ![[Screenshot 2023-05-12 at 2.24.07 pm.png]]

### f-statistic
- ![[Screenshot 2023-05-12 at 2.25.51 pm.png]]
- ![[Screenshot 2023-05-12 at 2.28.40 pm.png]]
- ![[Screenshot 2023-05-12 at 2.29.33 pm.png]]

### RSE
- ![[Screenshot 2023-05-12 at 2.50.05 pm.png]]

## matrix shit
- ![[Screenshot 2023-05-12 at 2.51.29 pm.png]]