# Lecture 1 

---
- oltp and olap, fact tables, dimension tables, business queries, data warehouse schemas, concept hierarchies, starnet 
- Why data warehouse and data mining?
	- explosive growth of data: from terabytes to petabytes 
- What is data warehouse and mining 
- OLAP and OLTP 

Relational databases 
	- support: delete, insert, update and query 
	- queries are often simple 
	- consistency/integrity is crucial

Data warehouses 
- mainly support "query"
- queries are more complex 

a relational database is a collection of tables, each assigned a unique name
- each table consists of a set of attributes and usually stores a large set of tuples (rows)
- columns or fields 

a diagram called an entity relationship is ofetn constructued for relational databases, it shows the schema and the relationship between multiple tables 
- square resembles table 
- circle is a field in that tuple 
- diamond is the relationship name, needs to be in verb form 

Purpose of relational databases 
- store data and retreive data

this is called Online Transaction Processing (OLTP)

relational databases are passive data repositories meaning it cant show you trends but only the data that is stored in that database 

Transactional database 
- consists of a file where each record represents a transaction 

Storing data in a data warehouse 
- data is stored in DBMS using tables 

what is a data warehouse 
- subject oriented 
	- focusing on the modeling and analysis of data for decision makers, not on daily operations or transaction processing 
	- provide a simply and concise view around particular subject issues by excluding data that isnt useful in the final decsision process
- integrated 
	- constructued by integrating multiple, heterogeneous data sources, such as relational databases, flat files, on-line transaction records 
- time-variant 
	- provides data from a longer time frame 
- non-volatile 
	- physically seperate store of data transformed from the operational environment 
	- operational update of data does not occur in the data warehouse environment 

Data warehouse (OLAP) vs Operational DBMS (OLTP)
- OLTP (on-line transaction processing)
	- does day-to-day operations like purchasing, inventory, banking and so on
	- many short queries 
	- update account balance is an examply 
- OLAP (on-line analytical processing)
	- data analysis and decision making 
	- long transactions, complex queries 
	- report total sales for each department in each month 
	- queires touch large amounts of data 
	- updates happen at spiratic intervals

doing oltp and olap in the same database is often impractical 
- different performance requirements 
- different data modelling requirements 
- analysis queries require data from many sources 

data warehouse models 
- enterprise warehouse 
	- collects all of the information about subjects spanning the entire organsiation 
	- contains both detailed and summarised data
- data mart 
	- contains a subset of data that is of value to a specific group of users 
- virtual warehouse 
	- set of views over operational databases 


