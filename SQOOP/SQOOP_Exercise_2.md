# Exercise 2

### Import stocks_eod to HDFS
sqoop import "-Dorg.apache.sqoop.splitter.allow_text_splitter=true" \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity \
--table stocks_eod \
--target-dir "/user/varunu28/exercise_import/stocks_eod"

								OR

### Import stocks_eod to HIVE
sqoop import "-Dorg.apache.sqoop.splitter.allow_text_splitter=true" \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse" \
--username nyse_ro \
--password itversity \
--table stocks_eod \
--hive-import \
--hive-database varunu28 \
--create-hive-table

### Running query to create table "stocks_revenue_monthly" in HIVE
create table stocks_revenue_monthly as
select stockticker, substr(tradedate, 1, 7) trademonth,
sum(volume) monthly_volume
from stocks_eod
group by stockticker, substr(tradedate, 1, 7);

### Creating SQL table
create table stocks_revenue_monthly_varun
(
stockticker varchar(10),
trademonth varchar (15),
monthly_volume bigint(25)
);

### Exporting from HIVE to MySQL
sqoop export \
--connect "jdbc:mysql://nn01.itversity.com:3306/nyse_export" \
--username nyse_ro \
--password itversity \
--table stocks_revenue_monthly_varun \
--export-dir "/apps/hive/warehouse/varunu28.db/stocks_revenue_monthly" \
--mysql-delimiters




