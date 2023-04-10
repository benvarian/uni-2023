## storing data in a data warehouse 
- more advanced database managemnt system for storing large amounts of data
- a data cube is used to support OLAP operations

## multi-dimensional view of data 
- (2d) ![[Screenshot 2023-03-09 at 7.19.10 pm.png]]
- (3d) ![[Screenshot 2023-03-09 at 7.19.21 pm.png]]
- data cube ![[Screenshot 2023-03-09 at 7.20.00 pm.png]]
- (5d data = many data cubes) ![[Screenshot 2023-03-09 at 7.22.12 pm.png]]

## data cube is a metaphor 
- data cube is a metaphor for multi-dimenstional data storage 
- the term hypercube is sometimes used
- actual storage of such data may be different from the logical representation 
- relational OLAP (ROLAP) 
	- an extended relational DBMS that maps operations on multidimensional data to standard relational operations 
- multidimensional OLAP (MOLAP)
	- a special-purpose server that directly implements multidimensional data and operations 
- difference 
	- ![[Screenshot 2023-03-09 at 7.24.40 pm.png]]

## from tables to data cubes 
- a dw is based on a multi-dimensional data model which views data in the form of a data cube 
- a data cube is organsied around a central theme, such as sales
- allows data to be modelled and viewed in multiple dimensions 
	- dimension tables, such as item (item stuff like brand, type ...)
	- fact table that contains measurements of a central theme (dollars sold, units sold) and keys to each of the related dimension tables 

## fact tables 
- contains measurements about a process of interest 
- each fact row contains 2 things 
	- numerical measure columns 
	- foreign keys to dimension tables 
- properties of fact tables 
	- very big 
		- millions or billions of rows
	- narrow 
		- small number of columns 
	- often append new rows to the fact table 
		- new events in the world -> new rows in the fact table 
- uses of fact tables 
	- obtain measurements from the fact table 
	- aggregate measurements from columns of the fact table 

### fact table and factless fact tables 
- ![[Screenshot 2023-03-09 at 7.29.40 pm.png]]

## grain of a fact table 
- grain of a fact table means **one fact table row** 
- maximum level of detail of the warehouse 
- example grain statements: (one row represents a..)
	- line item from a cash register receipt 
	- boarding pass to get on a flight 
	- student enrolled in a course 
- finer grained fact tables 
	- are more expensive 
	- have more rows 
- trade-off between performance and expensiveness 
	- rule of thumb: error in favor of expressiveness 
	- pre-computed aggregates can solve performance problems 

## measures 
- a data cube measure is numeric function that can be evaluated at each point in the data cube space 
- the value is computed for a given point by aggregating the data corresponding to the respective dimension-value pairs defining the given point 

### types of measures 
- distributive 
	- can be computed in a distributed manner by applying the same function on partitioned sets 
	- count(), min(), and max()
- algebraic 
	- can be computed by an algebraic function with M arguments, each of which is obtained by applying a distributive aggregate function 
	- avg(), standard_deviation()
- holistic 
	- if there is no fixed bound on the storage size required to define a subaggregate
	- median mode and rank
	- a masure is holistic if its acquired by using a holistic aggreagte function 

## dimension table
- each one corresponds to a real world object or concept 
- examples
	- customer
	- product 
	- date 
	- employee 
- properties of dimension tables 
	- contains many descriptve columns 
	- generally dont have too many rows 
	- contents are relatively static 
- use of dimension tables 
	- filters are based on dimension attributes 
	- grouping columns are dimension attributes 
	- fact tables are referenced through dimensions 
- **determine a candidate key based on the grain statement**
	- example: a student enrolled in a course 
	- (course, student, term) is a candidate key 
- add other relevant dimensions that are functionally determined by the candidate key 

### concept hierarch in dimensions 
- sales volume as a function of product, month, and region 
- ![[Screenshot 2023-03-09 at 9.07.17 pm.png]]

### the role of concept hierarchies 
- concept hierarchy 
	- defines a sequence of mappings form a set of low-level concepts to high-level, more general concepts 
- schema hierarchy 
	- a concept hierarchy that is a total or partial order among attributes in a database schema 
	- ex
		- total order: street < city < province_or_state < country
		- partial order: day < {month < quarter; week} < year
- set-grouping hierarchy 
	- defined by discretising or grouping values for a given dimension or attribute 

### example concept hierarchies: schema hierarchy 
- ![[Screenshot 2023-03-09 at 9.11.12 pm.png]]
- ![[Screenshot 2023-03-09 at 9.12.49 pm.png]]
- example of concept hierarchy for price 
	- ![[Screenshot 2023-03-09 at 9.13.18 pm.png]]

## facts vs dimension tables 
- facts
	- narrow 
	- big (many rows)
	- numeric 
	- growing over time 
- dimensions 
	- wide 
	- small (fewer rows)
	- descriptive 
	- static

## multi-dimensional data model 
- data cube
	- base cube, apex cube 
	- concept of hierarchies 
- schemas 
	- star
	- snowflake 
	- fact constellations 
- OLAP operations 
	- roll up, drill down, slice & dice, pivot 

## a starnet model of business queries 
- ![[Screenshot 2023-03-09 at 9.15.47 pm.png]]

## granularity of viewing the data warehouse 
- ![[Screenshot 2023-03-09 at 9.16.13 pm.png]]

## data warehouse design template 
- kimball's four steps 
	1. identify a business process to model 
		- eg: orders, invoices, shipments, sales
	2. determine the grain of the business process 
		- individual transactions, individual daily snapshots
	3. choose the dimensions that apply to fact table rows 
		- example dimensions are time, item, customer, supplier, transaction type and status 
	4. identify the measure that populates fact table rows 
		- typical measures are numeric additive quantities like dollars_sold and units_sold

## logical data warehouse design 
- logical design vs physical design 
	- logical design = conceptual organisation for the database 
		- create an abstraction for a real world process
	- physical design = how is the data stored 
		- select data structures (tables, indexes, materialised views)
		- organise data structures on disk 
- 3 main gaols for logical design 
	- simplicity 
	- expressiveness 
	- performance 

### goals for logical design 
- simplicity
	- users should understand the design
	- data model should match users conceptual model 
	- queries should be easy and intuitive to write
- expressiveness 
	- include enough info to answer important queries 
	- include all relevant data 
- performance 
	- an efficient physical design should be possible 

## schema 
- star schema 
	- a fact table in the middle connected to a set of dimension tables 
- snowflake schema 
	- some dimensional hierarchy is normalised into a set of smaller dimension tables, forming a shape similar to a snowflake 
	- reduces redundancy at the code of efficiency 
- galaxy schema (fact constellation)
	- multiple fact tables share dimension tables 
	- viewed as a collection of stars

### star schema 
- ![[Screenshot 2023-03-09 at 9.27.26 pm.png]]

#### star schema: ignore some fields 
- ![[Screenshot 2023-03-09 at 9.29.01 pm.png]]

#### star schema: representing data cube with four tables 
- ![[Screenshot 2023-03-09 at 9.29.26 pm.png]]

### snowflake schema 
- ![[Screenshot 2023-03-09 at 9.29.56 pm.png]]


## star schema vs snowflake schema 
- star schema 
	- fewer tables, faster when browsing data 
	- more redundant information 
- snowflake schema 
	- more tables, slower when browsing data
	- reduces redundancy 
- redundancy meaning 
	- more storage 
	- more work in data integratoin and cleaning 

## fact constellation - galaxy schema 
- ![[Screenshot 2023-03-09 at 9.31.24 pm.png]]

## typicall OLAP operations 
- roll up (drill up): summarise data 
	- by climbing up hierarchy or by dimension reduction
- drill down (roll down): reverse of roll up
	- from higher level summary to lower level summary or detailed data, or introducing new dimensions 
- slice and dice 
	- project and select 
- pivot (rotate)
	- reorient the cube, visualisation, 3d to series of 2d planes
- other operations 
	- drill across 
		- involving multiple fact tables 
	- drill through 
		- through the bottom level of the cube to its back-end relational tables 

### example of OLAP operations 
- ![[Screenshot 2023-03-09 at 9.36.09 pm.png]]

- roll up and drill down example
	- ![[Screenshot 2023-03-09 at 9.37.17 pm.png]]
- dice
	- ![[Screenshot 2023-03-09 at 9.37.43 pm.png]]
- slice 
- a subset of the data generated by picking a value for one dimension and only showing the data for that value (for instance only the data at one point in time)
- ![[Screenshot 2023-03-09 at 9.39.51 pm.png]]
- ![[Screenshot 2023-03-09 at 9.40.11 pm.png]]

### drill-across example
- question: how did actual sales diverge from forecasted sales in sep 19?
- drill across between forecase and sales 
- ![[Screenshot 2023-03-09 at 9.41.56 pm.png]]