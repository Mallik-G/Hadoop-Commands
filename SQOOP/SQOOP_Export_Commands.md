# SQOOP EXPORT

### Basic SQOOP Export Command
sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' 

### Basic SQOOP Export Command with specific columns
sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' \
--num-mappers 1 \
--columns order_id,order_date,order_customer_id,order_status

### SQOOP Export with a staging table
sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' \
--num-mappers 1 \
--columns order_id,order_date,order_customer_id,order_status \
--staging-table varunu28_orders_staging \
--clear-staging-table

### SQOOP Export with UPDATE KEY with UPDATE ONLY MODE
sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' \
--num-mappers 1 \
--columns order_id,order_date,order_customer_id,order_status \
--update-key order_id

### SQOOP Export with UPDATE KEY with allowinsert MODE
sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' \
--num-mappers 1 \
--columns order_id,order_date,order_customer_id,order_status \
--update-key order_id \
--update-mode allowinsert

