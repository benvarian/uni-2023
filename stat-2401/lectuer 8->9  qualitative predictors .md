- supposed that we wish to investigate differences in credit card balance between males and females
- if a qualitative predicots (known as a factor) only has two levels, then incorporating it into a regression model is very simple 
- simply create an indicator or dummy variable that takes on two possible numerical values 
- ![[Screenshot 2023-05-04 at 1.32.53 pm.png]]

- ![[Screenshot 2023-05-04 at 1.34.08 pm.png]]

- to do this we will seperate male and female from the column, by a 1 or 0, the incorporate it into the table 
	- ![[Screenshot 2023-05-04 at 1.34.52 pm.png]]

- ![[Screenshot 2023-05-04 at 1.35.35 pm.png]]
- these values interpret to be, the average credit card debt for males is 509.80 and for females carry an extra 19.73$ in additional debt, (this came from the if credit$gender == female).
- however the p value is very high, which indicates that there is no statistical evidence 


## when theres more than 2 factor variables 
- ![[Screenshot 2023-05-04 at 1.38.43 pm.png]]
- ![[Screenshot 2023-05-04 at 1.39.21 pm.png]]
- ![[Screenshot 2023-05-04 at 1.39.29 pm.png]]
- this means than $B{0}$  can be interpreted as the average credit card balance for african americans, B1 is the difference in the average balance between the asian and african americans, B2 the didference between the caucasian and african american categories 
- the level with no dummy variable which is "african american", 
	- ![[Screenshot 2023-05-04 at 1.44.15 pm.png]]
	- ![[Screenshot 2023-05-04 at 1.44.36 pm.png]]
	- so as the african american is the baseline, this shows that with the help of summary that  i1 is x less to have that amount of debt. 
	- however once again the p-value for these measurements is very high showing no statistical evidence that the two are linked. 
	- rather than rely on the individual coefficients, we can use an F-test to test H0: B1 = B2 = 0.
		- this f-test has a p-value of 0.9575, showing that we cannot reject the null hypothesis as there is no relationship between balance and ethnicity.
		- ![[Screenshot 2023-05-04 at 1.48.16 pm.png]]


## removing the additive assumption 
- for the example of the sales linear model 
- it states that the average effect on sales of a one-unit increase in TV is always B1, regardless of th eamount of money spent on radio 
- however, this simple model may be incorrect. Suppose that spending money on radio advertising actually increases the effectiveness of TV advertising, so that the slope term for TV should increase as radio increases. 
	- in this situation, given a fixed budget of 100k, spending half on radio and half on tv may increase sales more than allocating the entire amount to either TV or to radio. 
- in marketing this is known as a synergy effect, and in statistics it is referred to as an interation effect. 
- ![[Screenshot 2023-05-04 at 2.22.15 pm.png]]
- for example, say that we are interested in studyng the productivity of a factory.
	- want to predict the number of units produced on the basis of the number of production lines and the total number of workers 
	- it seems likely that the effect of increasing the number of production lines will depend on the number of workers, since if no workers are available to operate the lines, then increasing the number of lines will not increase prodution. 
	- this suggests that it would be appropriate to include an **interaction** term between lines and workers in a linear model to predict units 
	- ![[Screenshot 2023-05-04 at 2.32.47 pm.png]]

- returning to the advertising example 
	- a new linear model that uses radio, tv, and an interaction between the two to predict sales takes the 
		- ![[Screenshot 2023-05-04 at 2.34.21 pm.png]]
		- interpret B3 as the increase in the effectiveness of TV advertising for a one unit increase in radio advertising 
	- ![[Screenshot 2023-05-04 at 2.35.38 pm.png]]
		- the results strongly suggest that the model that includes the interaction term is superior to the model that contains only main effects 
		- the p-value for the interaction term, TV x radio, is extremely low, indicating that there is strong evidence for H1: B3 ≠ 0. In other words,  it is clear that the true relationship is not additive 
		- the $R^2$ for the model is 96.78%. compared to only 89.72% for the model that predicts sales using TV and radio without an interaction term 

## analysis of covariance (ANCOVA)
- consider the situation in which we want to model a response variable, Y based on a continuous predictor, X and a dummy variable, Z. say the effect of X on Y is linear. This situation is the simplest version of what is commonly referred to as analysis of covariance, **as the predictors include both quantitative variables and qualitative variables**
	- ![[Screenshot 2023-05-04 at 2.54.34 pm.png]]
- there are 4 possible models based on Z
	- coincident regression lines/simple regression models 
		- the simplest model in the given situatoin is one in which the dummy variable Z has no effect on Y (both B2 = B3 = 0). that is, and the regression line is exactly the same for both values of the dummy variable. That is 
			- Y = B0 + B1X + e
	- parallel regression lines/parallel regression models 
		- another model to consider for this situation is one in which the dummy variable produces only an additive change in Y (B2 ≠ 0 & B3 = 0)
			- ![[Screenshot 2023-05-04 at 2.56.58 pm.png]]
		- the regression coefficient B2 measures the additive change in Y due to the dummy variable 
	- regression lines with equal intercepts but different slopes 
		- the dummy variable only changes the size of the effct of X on Y (B2 = 0 & B3 ≠ 0)
			- ![[Screenshot 2023-05-04 at 2.58.14 pm.png]]
		- rarely considered since it isnt that interesting to focus on equal intercepts 
	- unrelated regression lines/seperate regression models 
		- the most general model is appropriate when the dummy variable produces an additive change in Y and also changes the size of the effect of X on Y (B2 ≠ 0 & B3 ≠ 0).
			- ![[Screenshot 2023-05-04 at 3.24.44 pm.png]]
	- in summary we have the following models under the following conditions 
		- ![[Screenshot 2023-05-04 at 3.25.14 pm.png]]

- extract the p-value with high precision 
	- anova(M1,M2)$'Pr(>F)'[2]