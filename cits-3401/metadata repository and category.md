
- metedata is collectively organised in a catalogue called metadata repository 
- it stores descriptive information about data model used to store and share 

- each data warehouse has one or multiple repositories that hold the following metadata in them
	- definition of the structure of the data warehouse 
	- structure of the table involved in the warehouse 
	- description of the dataflow through the warehouse 
	- outcomes of all querying process
	- information about who accesses objects and when 
	- includes aggregation, summarising  


- metadata categories 
	- broadly categories into three categories 
	- business metadata
		- includes data ownership information, business definition and changing policies 
		- contains high level definitions of all fields present in the data warehouse 
	- operational metadata 
		- offers a connection between the metadata repository and the data warehouse 
		- enables easier use for businesses and technical customers 
		- benefits 
			- referenced at a row level of granularity in DW
			- provides a detaield row level explanation of actual information content 
	- technical metadata 
		- structural information such as primary and foreign key attributes and indices data types and values
		- gives information about the structure of data, where it resides, and other technical details related to finding data in its native database 
		- used by software tools to understand and process data 

- ![[Screenshot 2023-04-26 at 9.50.32 pm.png]]

