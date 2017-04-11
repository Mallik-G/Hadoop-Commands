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

### Import command with SELECTED COLUMNS
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_import" \
--username retail_dba \
--password itversity \
--table order_items_no_pk_varun \
--warehouse-dir "/user/varunu28/retail_db" \
--split-by order_item_id \
--boundary-query "SELECT MIN(order_item_id), MAX(order_item_id) FROM order_items_no_pk_varun WHERE order_item_id not in (10000000)" \
--delete-target-dir \
--columns "order_item_id, order_item_order_id, order_item_product_id, order_item_quantity, order_item_subtotal"

### Import command for COMPRESSION (DEFAULT)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--warehouse-dir "/user/varunu28/retail_db" \
--delete-target-dir \
--compress

### Import command for COMPRESSION (SNAPPY CODEC)
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--warehouse-dir "/user/varunu28/retail_db" \
--delete-target-dir \
--compression-codec org.apache.hadoop.io.compress.SnappyCodec
 
# Import command through Query
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--query "SELECT * FROM order_items where \$CONDITIONS" \
--target-dir "/user/varunu28/retail_db/order_items" \
--delete-target-dir \
--split-by order_item_id

# Import command using WHERE condition
sqoop import --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--table order_items \
--target-dir "/user/varunu28/retail_db/order_items" \
--delete-target-dir \
--where "order_item_order_id between 1 and 10 or order_item_order_id between 100 and 10000"


