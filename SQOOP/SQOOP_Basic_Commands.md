# SQOOP Basic Commands

### Command to list all databases using SQOOP 
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306" \
--username retail_dba \
--password itversity

### Command to list all databases using SQOOP along with log generation
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306" \
--username retail_dba \
--password itversity 2>sqoop-list-databases.log

### Command to list all databases using SQOOP along with log generation along with append to existing log
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306" \
--username retail_dba \
--password itversity 2>>sqoop-list-databases.log

### Command to list all databases using SQOOP along with log generation and data generation
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306" \
--username retail_dba \
--password itversity 2>sqoop-list-databases.log 1>sqoop-list-databases.data


### Command to list all tables in a database(retail_db) using SQOOP 
sqoop list-tables \
--connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity

### EVAL command to query a table in a database using SQOOP 
sqoop eval \
--connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--query "SELECT COUNT(1) FROM order_items"
