# SQOOP Import Commands

### Import command to import a SQL table to a directory by giving target directory path (The path should not already exist)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--target-dir "/user/varunu28/retail_db/order_items"

### Import command to import a SQL table to a directory by giving warehouse directory path (The directory name would be same as table name)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table products \
--warehouse-dir "/user/varunu28/retail_db"

