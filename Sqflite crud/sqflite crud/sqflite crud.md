# SQl
%%* setup sqflite
* open database
* create table
* perform crud%% 



sequelize 

```
npm install sequelize package
```
then we need to add the driver for work with databases, so install mysql2


```
npm install mysql2
```


nextly import
```
```const sequelize=require('sequelize');

```
we dont neeed to import mysql2 package as it works internally



## SQL
structured query language is query language used to communicate with RDBMS
for eg

 * data is stored in dbms as tables
 *  we created a data of student ie table of  data which contains details of student
 * the student is an entity, entity means student can have multiple properties such as student name,roll number,class, likely teacher is also an entity
 * these datas with entities have to be identified first, then we define them structure & data
 * structure consist of student name,roll number, class
 * data consist of the values of structure such 'rahul',23,5a
 * all these cosnist inside a Rdbms, so inorder to get a particular conditioned data we use sql
 
 








# SQL


### CREATE
To create a table in sql for example for creatring a table named products

```
CREATE TABLE products(id INT NOT NULL,
name STRING,
price MONEY,
PRIMARY KEY(id))

```
* this command create a table named products
* queries are written in CAPITAL
* id INT NOT NULL   -- this creates a column with which is a required fied while adding new data
*  PRIMARY KEY(id)-- this mentions this is an unique column ,so no duplicates .

```
INSERT INTO products VALUES(1,"Pen",20)
```
adds new data in to sql database in order to column

```
INSERT INTO products(id,name) VALUES(2,"pencil")
```

to add value to table with only specific columns


### READ


To read the entire table
```
SELECT * FROM products 
```

this will result entire table to show





```
SELECT (name) FROM products
```
to select a particular column from a table


#### Where
inoder to select a particular row value or a conditioned value , we need to use the Where condition
```
SELECT * FROM products WHERE(name='Pen')
```
 this will give us  row named Pen


### UPDATE


value of the column will be assigned to new val
for updating data in a table
```
UPDATE products SET name='Tea' WHERE id=2
```

we need to use WHERE condition else entire value will be assigned


To add new column into a table
```
ALTER TABLE products ADD stock INT
```



### DELETE
 to delete an data from table use
 ```

DELETE FROM products WHERE name="pencil"
```

above query will delete the entire row ,
to ddelete the entire table



```

ALTER TABLE products
DROP COLUMN stock

```











