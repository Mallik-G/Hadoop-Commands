# HIVE DDL COMMANDS

### Command to create an EXTERNAL table
CREATE EXTERNAL TABLE stocks_eod_external
(
  stockticker string,
  tradedate int,
  openprice float,
  highprice float,
  lowprice float,
  closeprice float,
  volume bigint
)
row format DELIMITED fields TERMINATED BY ','
STORED AS textfile
location '/user/varunu28/nyse';

### Command to create a MANAGED table
CREATE TABLE stocks_eod_managed
(
  stockticker string,
  tradedate int,
  openprice float,
  highprice float,
  lowprice float,
  closeprice float,
  volume bigint
)
row format DELIMITED fields TERMINATED BY ','
STORED AS textfile
location '/user/varunu28/nyse';