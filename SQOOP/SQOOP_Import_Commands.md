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

### Import command to import a SQL table to an existing directory by using APPEND
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--warehouse-dir "/user/varunu28/retail_db" \
--append

### Sequence file format while importing (Text being the default file format)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--target-dir "/user/varunu28/retail_db/order_items_seq" \
--as-sequencefile

### Avro file format while importing (Text being the default file format)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--target-dir "/user/varunu28/retail_db/order_items_avro" \
--as-avrodatafile

### Import command to import a SQL table which does not have a primary key (Using SPLIT BY)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_import" \
--username retail_dba \
--password itversity \
--table order_items_no_pk_varun \
--warehouse-dir "/user/varunu28/retail_db" \
--split-by order_item_id

### Import command to import a SQL table which does not have a primary key (Using num of mappers as 1. Can use "--m 1" also)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_import" \
--username retail_dba \
--password itversity \
--table order_items_no_pk_varun \
--warehouse-dir "/user/varunu28/retail_db" \
--num-mappers 1 

### Import command to import a SQL table which may/maynot have a primary key (Using autoreset-to-one-mapper )
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_import" \
--username retail_dba \
--password itversity \
--table order_items_no_pk_varun \
--warehouse-dir "/user/varunu28/retail_db" \
--autoreset-to-one-mapper 

### Import command with a BOUNDARY QUERY
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_import" \
--username retail_dba \
--password itversity \
--table order_items_no_pk_varun \
--warehouse-dir "/user/varunu28/retail_db" \
--split-by order_item_id \
--boundary-query "SELECT MIN(order_item_id), MAX(order_item_id) FROM order_items_no_pk_varun WHERE order_item_id not in (10000000)"


 

