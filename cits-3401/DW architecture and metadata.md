- data warehouse metadata 
	- metadata that describes tables typicaly includes 
		- physical and logical name 
		- type: fact, dimension
		- role: legacy, OLTP, stage 
		- DBMS: DB2, informix, MS SQL server, Oracle
		- definition/description 
		- location 
- metdata describes columns within table 
	- physical and logical name 
	- order in table 
	- datatype 
	- legnth 
	- default value 
	- nullable/required 
	- edit rules

![[metadata in data warehousing]]

- data definition and mapping metadata 
	- list of all columns from every table in the DDS, ODS, and NDS along with their meaning and values 
	- data definition metadata uses the table key and column key defined in the data structure metadata 

- mapping metadata
	- describes where each piece of data comes from in the source system
	- also known as data lineage metadata

- metadata example 
	- ![[Screenshot 2023-04-26 at 4.50.30 pm.png]]

![[metadata repository and category]]

![[application of metadata in DW]]

![[roles of metadata]]

![[challenges for metadata management]]
