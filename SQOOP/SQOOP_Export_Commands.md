# SQOOP EXPORT

sqoop export --connect "jdbc:mysql://nn01.itversity.com:3306/retail_export" \
--username retail_dba \
--password itversity \
--export-dir /user/varunu28/retail_db/orders \
--table varunu28_orders \
--input-fields-terminated-by '|' 
