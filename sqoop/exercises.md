#sqoop exercise 09231 younghun knag 강영훈
##1

1-1.catch column
sqoop eval \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training \
--query "describe accounts"
---------------------------------------------------------------------------------------------------------
| Field                | Type                 | Null | Key | Default              | Extra                | 
---------------------------------------------------------------------------------------------------------
| acct_num             | int(11)              | NO  | PRI | (null)               |                      | 
| acct_create_dt       | datetime             | NO  |     | (null)               |                      | 
| acct_close_dt        | datetime             | YES |     | (null)               |                      | 
| first_name           | varchar(255)         | NO  |     | (null)               |                      | 
| last_name            | varchar(255)         | NO  |     | (null)               |                      | 
| address              | varchar(255)         | NO  |     | (null)               |                      | 
| city                 | varchar(255)         | NO  |     | (null)               |                      | 
| state                | varchar(255)         | NO  |     | (null)               |                      | 
| zipcode              | varchar(255)         | NO  |     | (null)               |                      | 
| phone_number         | varchar(255)         | NO  |     | (null)               |                      | 
| created              | datetime             | NO  |     | (null)               |                      | 
| modified             | datetime             | NO  |     | (null)               |                      | 
---------------------------------------------------------------------------------------------------------


1-2.
sqoop import \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training \
--table accounts \
--columns "acct_num, first_name, last_name" \
--target-dir /loudacre/accounts/user_info \
--as-textfile \


##1.end


##2

2 
sqoop import \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training \
--table accounts \
--columns "acct_num, first_name, last_name" \
--target-dir /loudacre/accounts/user_compressed \
--as-parquetfile \
--compression-codec org.apache.hadoop.io.compress.SnappyCodec


##2.end

##3
3 
sqoop import \
--connect jdbc:mysql://localhost/loudacre \
--username training --password training \
--table accounts \
--where "state='CA'" \
--target-dir /loudacre/accounts/CA \
--as-parquetfile -z
##3.end
#.end