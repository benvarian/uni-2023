## where to store data
- relational databases 
	- supports crud and querys 
	- consistency/integrity is crucial 
	- queries are often simple 
	- data from single department/organisation
- Data warehouses 
	- mainly support querys 
	- queries are more complex 

## storing data in a relational database 
- a realational database is a collection of tables 
- each assigned a unique name 
- each table consists of a set of attributes (columns or fields) and usually stores a large set of tuples (rows or records)
- each tuple in a relational table represents an object identified by a unique key and described by a set of attribute values 
- ![[Screenshot 2023-03-01 at 4.29.29 pm.png]]

- a data model called, **entity relationship** (ER), is often constructed to represent databases 
- ![[Screenshot 2023-03-01 at 4.32.29 pm.png]]
- data accessed by languages like SQL
- a given query is transformed into a set of relational operation such as join, selection and projection, and is then optimised for efficient processing 
- efficiency of retrieval, efficiency of update and integrity are the key requirements of a good db

## purpose of relational databases 
- store data correctly and retrieve data on demand 
- this type of processing is sometimes called online transaction processing (OLTP)
- relational databases are passive data repos, this means the query can only show you what is stored on the db and cant explain trends or the meaning of the data 
- query answering in relational databases 
	- ![[Screenshot 2023-03-01 at 4.36.12 pm.png]]

## transactional database 
- consists of a file where each record represnets a transaction 
- supports nested relations 

## storing data in a data warehouse 
- data comes from multiple data sources 
- data are stored in DBMS using tables 
- query answering process is more complex 
	- ![[Screenshot 2023-03-01 at 4.37.41 pm.png]]

## what is a data warehouse 
- subject-oriented, integrated, time-variant and non-volatile 
### data warehouse - subject oriented 
- organised around major subjects, such as customer, supplier, product, sales and time 
- focus on the modeling and analysis of data for decision makers, not on daily operations or transaction processing 
- provide a simple and concise view around particular subject issues by excluding data that are not useful in the decision making process
### data warehouse - integrated 
- construced by integrating multiple heterogeneous data sources 
- data cleaning and data integration techniques are applied 
- data warehouses combine data from multiple sources 
- data must be translated into a consistent format 
- reasons as to why data integration is hard 
	- metadata is poor or non-existent 
	- data quality is often bad 
		- missing values 
		- multiple spellings of the same thing 

### data warehouse - time variant 
- the time horizon for the data warehouse is significaltly longer than that of operational DB systems 
- every key structure in the data warehouse 

### data warehouse - non-volatile 
- a phyiscally sperate store of data transformed from the operational environment 
- operational update of data does not occur in the data warehouse environment 
- **the previous data is not erased when new data is added to it. A data warehouse is kept separate from the operational database and therefore frequent changes in operational database is not reflected in the data warehouse.**


## Data warehouse (OLAP) vs Operational DBMS (OLTP)
- OLTP (on-line transaction processing)
	- major task of traditional/operational relational DBMS 
	- day-to-day operations, purchasing, inventory, banking 
	- **type of data processing that consists of executing a number of transactions occuring concurrently**
	- ex 
		- online banking 
		- shopping 
		- order entry
		- sending text messages
- OLAP (on-line analytical processing)
	- major task of data warehouse system 
	- data analysis and decision making 
	- can organise and present data in various forms and combinations 
	- **type of software that allows users to analyse information from multiple database systems at the same time**
	- updates are infrequent

## why OLAP & OLTP dont mix 
- transaction processing (OLTP)
	- fast reponse time important
	- <1 second 
	- data must be up-to-date 
	- consistent at all times 
	- normalised schema for consistency 
	- limited number of standardies queries and updates 
- Data analysis (OLAP)
	- queries can consume lots of resources 
	- can saturate CPUs and disk bandwith 
	- simplicity of data model is important 
	- de-normalised schemas are common 
		- fewer joins -> improved query performance 
		- fewer tables -> schema is easier to understand 
-  a OLTP system targets one specfic process 
- OLAP integrates data from different processes 
	- combine sales, inventory and purchasing data 
	- analyse experiments conducted by different labs 
- OLAP often makes use of historical data 
	- identify long-term patterns 
	- id changes over time 


## why seperate data warehouse 
- doing OLTP and OLAP in the same database system is often impractical 
	- diff performance requirements 
	- diff data modeling requirements 
	- analysis queries require data from many sources 
- different functions and different data:
	- missing data: decision support requires historical data which opertaional DBs do not typically maintain 
	- data consolidation: DW requires consolidation of data from heterogeneous soruces 
	- data quality: different sources typicall use inconsistent data representations, codes and formats which have to be reconciled 

## comparison of OLTP and OLAP 
- ![[Screenshot 2023-03-01 at 4.59.59 pm.png]]

## building a data warehouse along with OLTP systems 
- build a data warehouse
	- copy data from varous OLTP systems 
	- optimise data organisation, system tuning for OLAP
	- transactions aren't slowed by big analysis queries 
	- periodically refresh the data in the warehouse 
- high performance for both systems 
	- DBMS - tuned for OLTP 
	- Warehouse - tuned for OLAP, complex queries, multidimensional view 

## a 3 tier data warehousing architecture 
- ![[Screenshot 2023-03-01 at 5.02.08 pm.png]]

## data warehouse models
- enterprise warehouse 
	- an enterprise warehouse colects all of the information about subjects spanning the entire organsation 
	- contains both detailed and summerised data 
- data mart 
	- contains a subset of corporate-wide data that is of value to a specific group of users 
	- scope is confined to specific subjects 
- virtual warehouse 
	- a set of views over operational databases 
	- for efficient query processing only some of the possible summary views may be materialised 

## data warehouse of all electronics 
- a data warehouse is a repository of information collected from multiple sources, stored under a unified schema, usually resides at a single file 
- provide analysis of the companys sales per item type per branch for a specified period 
- ![[Screenshot 2023-03-01 at 5.06.28 pm.png]]

## Federated databases 
- alternative to data warehouses 
- pulls data from source systems as needed to answer queries 
- lazy vs eager data integration 
	- ![[Screenshot 2023-03-01 at 5.08.31 pm.png]]

## warehouse vs federation 
- advantages of federated databases 
	- no redundant copying of data 
	- queries see real time view of evolving data 
	- more flexing security policy 
- disadvantages of federeated databases 
	- analysis queries place extra load on transactional systems 
	- query optimisation is hard to do well
	- historical data may not be available 
	- complex wrappers needed to mediate between analysis server and source systems 
- data warehouses are much more common in practice 
	- better performance 
	- lower complexity 
	- slightly out of date data is acceptable 

## 3 kinda of data warehouse applications 
- information processing 
	- supports querying 
	- basic stat analysis 
	- reporting using crosstabs 
- analytical processing 
	- multidimensional analysis of data warehouse data
	- supports basic OLAP operations, slice-dice, drilling, pivoting 
- data mining 
	- knowledge discovery form hidden patterns 
	- supports associations 
	- constructing analytical models 
	- performing classification and prediction 

## why data mining 
- the explosive growth of data, from terabytes to petabytes 
	- data explosion
		- capability of generating, collecting, storing and managing data has grown tremendously in the last 50 years 
	- data collection and data availability 
		- automated data collection tools, databse systems, web, computersied society 
	- major sources of abundant data 
		- business: web, e-commerce, transactions, stocks 
		- science: remote sensing, bioinformatics, scientific simulations
		- society and everyone else: news, digital cameras
- key points 
	- far exceeded human ability for comprehension 
	- manual knowledge extraction is prone to bisases and errors, and is extremenly costly and time consuming 
	- data mining tools perform data analysis and uncover important data patterns, contributing greatly to business strategies, knowledge bases and scientific and medical research 

## what is data mining 
- extraction of interesitng patterns or knowledge form a huge amount of data 
- alternative names 
	- knowledge discovery 

## data mining in different data sources 
- structured and semi-structured data 
	- relational database/ object relational data 
	- data warehouse 
	- transactional database 
- unstructured data 
	- data streams and sensor data 
	- text data 
	- time series data 

## data mining: confluence of multiple disciplines 
- ![[Screenshot 2023-03-01 at 5.22.03 pm.png]]

## Steps of knowledge discovery from data (KDD) process
- ![[Screenshot 2023-03-01 at 5.22.31 pm.png]]

## techniques in the process
- ![[Screenshot 2023-03-01 at 5.22.48 pm.png]]

## coupling DM with DB/Dw systems 
- no coupling 
	- flat file processing 
	- is a poor design as may spend much time in pre-processing 
- loose coupling 
	- fetching data from DB/DW. mining does not explore data structure and optimisation methods provided by databases & data warehouse, difficult for high scalability 
- semi-tight coupling - enhanced DM performance 
	- provide efficient implementation for a few data mining primitives in a DB/DW system
- tight coupling 
	- DM is smoothly integrated into a DB/Dw system, mining query is optimised based on mining query, indexing, processing methods 