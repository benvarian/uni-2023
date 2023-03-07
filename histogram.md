## data visualisation 
- after getting the data and analysing it, we need to display and describe it 
- done differently for quantitative and categorical data 

## divide into bins 
- the range of values is divided into non-overlapping, equal-sized bins 
- the number of observations that lie in each bin is counted 
- the resulting data is presented as a table or a histogram 

## elephant data 
- as a running example to illustrate commands in R, assume that elephant is a data table with 41 rows and columns **age** and **matings** 
- as the elephant data is discrete with only 10 distinct values, it is natural to have just 10 bins 
- ![[Screenshot 2023-03-07 at 12.49.50 pm.png]]

## tables 
- for each possible value of m, we determine 
	- frequency - number of elephants with m matings, and 
	- relative frequency - percentage of elephants with m matings 
- R command table(elephant$Matings)
- ![[Screenshot 2023-03-07 at 12.51.28 pm.png]]
- hist(elephant$Matings)
- ![[Screenshot 2023-03-07 at 12.53.10 pm.png]]

## the iris data 
- the shape of the iris data is different to that of the elephant data 
	- the elephant values cluster around the "middle hump"
	- the petal width distribution is not all symmetric 
	- the petal width distribution has two "humps"

## mean
- the mean is the numeric average of the values 
- if the histogram were a solid object, then the mean is the value at which it would perfectly balance on a point 
- ![[Screenshot 2023-03-07 at 12.55.39 pm.png]]
- extreme values contribute to the mean more than the central values