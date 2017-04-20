# Sqoop Import Exercises

### List databases from retail_db
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity 

### List databases from nyse
sqoop list-databases \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity 

### List tables from retail_db
sqoop list-tables \
--connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity 

### List tables from nyse
sqoop list-tables \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity 

### Import all tables from retail_db to HDFS
sqoop import-all-tables --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--warehouse-dir /user/varunu28/exercise_import/text_format 

### Import all tables from retail_db to HDFS in avro format
sqoop import-all-tables --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--warehouse-dir /user/varunu28/exercise_import/avro_format \
--as-avrodatafile

### Import all tables from retail_db to Hive with delimiter as '|'
sqoop import-all-tables --connect "jdbc:mysql://nn01.itversity.com:3306/retail_db" \
--username retail_dba \
--password itversity \
--hive-import \
--hive-database varunu28
--fields-terminated-by '|'

### Import nyse.stocks_eod to HDFS using snappy codec compression and 8 parallel threads
// Solution 1 by using split-by 

sqoop import -m 8 \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity \
--table stocks_eod \
--warehouse-dir /user/varunu28/exercise_import/nyse_import \
--compress \
--compression-codec org.apache.hadoop.io.compress.SnappyCodec \
--split-by tradedate

// Solution 2 by giving Dorg parameter in sqoop import command 

sqoop import "-Dorg.apache.sqoop.splitter.allow_text_splitter=true" \
--m 8 \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity \
--table stocks_eod \
--warehouse-dir /user/varunu28/exercise_import/nyse_import \
--compress \
--compression-codec org.apache.hadoop.io.compress.SnappyCodec 
