# Mysql学习笔记
[返回-首页](../README.md)

## 1. Python连接Mysql


```python
import pymysql
import pandas as pd
```


```python
conn = pymysql.connect(host = '172.17.0.1',port = 12306,user = 'root',password = '********',db = 'mysql',charset='utf8')
```


```python
sql_query='select * from user'
content_df=pd.read_sql(sql_query,con=conn)
```


```python
content_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Host</th>
      <th>User</th>
      <th>Password</th>
      <th>Select_priv</th>
      <th>Insert_priv</th>
      <th>Update_priv</th>
      <th>Delete_priv</th>
      <th>Create_priv</th>
      <th>Drop_priv</th>
      <th>Reload_priv</th>
      <th>...</th>
      <th>max_questions</th>
      <th>max_updates</th>
      <th>max_connections</th>
      <th>max_user_connections</th>
      <th>plugin</th>
      <th>authentication_string</th>
      <th>password_expired</th>
      <th>is_role</th>
      <th>default_role</th>
      <th>max_statement_time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>localhost</td>
      <td>root</td>
      <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>mysql_native_password</td>
      <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
      <td>N</td>
      <td>N</td>
      <td></td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>%</td>
      <td>root</td>
      <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>mysql_native_password</td>
      <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
      <td>N</td>
      <td>N</td>
      <td></td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 47 columns</p>
</div>



* 关闭连接


```python
conn.close()
```

## 2. Mysql客户端连接和管理


```bash
%%bash
mysqladmin --version
```

    mysqladmin  Ver 8.42 Distrib 5.7.29, for Linux on x86_64



```bash
%%bash
mysql -h 172.17.0.1 -P 12306 -uroot -p******** <<!
show databases;
!
```

    Database
    information_schema
    mysql
    performance_schema


    mysql: [Warning] Using a password on the command line interface can be insecure.


## 3. 修改密码 

在mysql的服务器本机上执行
```bash
mysqladmin -u root -p old_password password "new_password";
```

## 4. ipython连接管理mysql


```python
%load_ext sql
%sql mysql+pymysql://root:********@172.17.0.1:12306
```

    The sql extension is already loaded. To reload it, use:
      %reload_ext sql





    'Connected: root@None'




```python
%%sql
show databases;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    3 rows affected.





<table>
    <tr>
        <th>Database</th>
    </tr>
    <tr>
        <td>information_schema</td>
    </tr>
    <tr>
        <td>mysql</td>
    </tr>
    <tr>
        <td>performance_schema</td>
    </tr>
</table>




```python
%%sql
use mysql;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.





    []




```python
%%sql
show tables;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    31 rows affected.





<table>
    <tr>
        <th>Tables_in_mysql</th>
    </tr>
    <tr>
        <td>column_stats</td>
    </tr>
    <tr>
        <td>columns_priv</td>
    </tr>
    <tr>
        <td>db</td>
    </tr>
    <tr>
        <td>event</td>
    </tr>
    <tr>
        <td>func</td>
    </tr>
    <tr>
        <td>general_log</td>
    </tr>
    <tr>
        <td>global_priv</td>
    </tr>
    <tr>
        <td>gtid_slave_pos</td>
    </tr>
    <tr>
        <td>help_category</td>
    </tr>
    <tr>
        <td>help_keyword</td>
    </tr>
    <tr>
        <td>help_relation</td>
    </tr>
    <tr>
        <td>help_topic</td>
    </tr>
    <tr>
        <td>index_stats</td>
    </tr>
    <tr>
        <td>innodb_index_stats</td>
    </tr>
    <tr>
        <td>innodb_table_stats</td>
    </tr>
    <tr>
        <td>plugin</td>
    </tr>
    <tr>
        <td>proc</td>
    </tr>
    <tr>
        <td>procs_priv</td>
    </tr>
    <tr>
        <td>proxies_priv</td>
    </tr>
    <tr>
        <td>roles_mapping</td>
    </tr>
    <tr>
        <td>servers</td>
    </tr>
    <tr>
        <td>slow_log</td>
    </tr>
    <tr>
        <td>table_stats</td>
    </tr>
    <tr>
        <td>tables_priv</td>
    </tr>
    <tr>
        <td>time_zone</td>
    </tr>
    <tr>
        <td>time_zone_leap_second</td>
    </tr>
    <tr>
        <td>time_zone_name</td>
    </tr>
    <tr>
        <td>time_zone_transition</td>
    </tr>
    <tr>
        <td>time_zone_transition_type</td>
    </tr>
    <tr>
        <td>transaction_registry</td>
    </tr>
    <tr>
        <td>user</td>
    </tr>
</table>




```python
%%sql
show columns from user;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
    47 rows affected.





<table>
    <tr>
        <th>Field</th>
        <th>Type</th>
        <th>Null</th>
        <th>Key</th>
        <th>Default</th>
        <th>Extra</th>
    </tr>
    <tr>
        <td>Host</td>
        <td>char(60)</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>User</td>
        <td>char(80)</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>Password</td>
        <td>longtext</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Select_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Insert_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Update_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Delete_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Drop_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Reload_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Shutdown_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Process_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>File_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Grant_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>References_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Index_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Alter_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Show_db_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Super_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_tmp_table_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Lock_tables_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Execute_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Repl_slave_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Repl_client_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_view_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Show_view_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_routine_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Alter_routine_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_user_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Event_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Trigger_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Create_tablespace_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>Delete_history_priv</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>ssl_type</td>
        <td>varchar(9)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>ssl_cipher</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>x509_issuer</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>x509_subject</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>max_questions</td>
        <td>bigint(20) unsigned</td>
        <td>NO</td>
        <td></td>
        <td>0</td>
        <td></td>
    </tr>
    <tr>
        <td>max_updates</td>
        <td>bigint(20) unsigned</td>
        <td>NO</td>
        <td></td>
        <td>0</td>
        <td></td>
    </tr>
    <tr>
        <td>max_connections</td>
        <td>bigint(20) unsigned</td>
        <td>NO</td>
        <td></td>
        <td>0</td>
        <td></td>
    </tr>
    <tr>
        <td>max_user_connections</td>
        <td>bigint(21)</td>
        <td>NO</td>
        <td></td>
        <td>0</td>
        <td></td>
    </tr>
    <tr>
        <td>plugin</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>authentication_string</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>password_expired</td>
        <td>varchar(1)</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>is_role</td>
        <td>varchar(1)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>default_role</td>
        <td>longtext</td>
        <td>NO</td>
        <td></td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>max_statement_time</td>
        <td>decimal(12,6)</td>
        <td>NO</td>
        <td></td>
        <td>0.000000</td>
        <td></td>
    </tr>
</table>




```python
%%sql
select * from user;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
    2 rows affected.





<table>
    <tr>
        <th>Host</th>
        <th>User</th>
        <th>Password</th>
        <th>Select_priv</th>
        <th>Insert_priv</th>
        <th>Update_priv</th>
        <th>Delete_priv</th>
        <th>Create_priv</th>
        <th>Drop_priv</th>
        <th>Reload_priv</th>
        <th>Shutdown_priv</th>
        <th>Process_priv</th>
        <th>File_priv</th>
        <th>Grant_priv</th>
        <th>References_priv</th>
        <th>Index_priv</th>
        <th>Alter_priv</th>
        <th>Show_db_priv</th>
        <th>Super_priv</th>
        <th>Create_tmp_table_priv</th>
        <th>Lock_tables_priv</th>
        <th>Execute_priv</th>
        <th>Repl_slave_priv</th>
        <th>Repl_client_priv</th>
        <th>Create_view_priv</th>
        <th>Show_view_priv</th>
        <th>Create_routine_priv</th>
        <th>Alter_routine_priv</th>
        <th>Create_user_priv</th>
        <th>Event_priv</th>
        <th>Trigger_priv</th>
        <th>Create_tablespace_priv</th>
        <th>Delete_history_priv</th>
        <th>ssl_type</th>
        <th>ssl_cipher</th>
        <th>x509_issuer</th>
        <th>x509_subject</th>
        <th>max_questions</th>
        <th>max_updates</th>
        <th>max_connections</th>
        <th>max_user_connections</th>
        <th>plugin</th>
        <th>authentication_string</th>
        <th>password_expired</th>
        <th>is_role</th>
        <th>default_role</th>
        <th>max_statement_time</th>
    </tr>
    <tr>
        <td>localhost</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
</table>




```python
%%sql
show table status from mysql like 'user'
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    1 rows affected.





<table>
    <tr>
        <th>Name</th>
        <th>Engine</th>
        <th>Version</th>
        <th>Row_format</th>
        <th>Rows</th>
        <th>Avg_row_length</th>
        <th>Data_length</th>
        <th>Max_data_length</th>
        <th>Index_length</th>
        <th>Data_free</th>
        <th>Auto_increment</th>
        <th>Create_time</th>
        <th>Update_time</th>
        <th>Check_time</th>
        <th>Collation</th>
        <th>Checksum</th>
        <th>Create_options</th>
        <th>Comment</th>
        <th>Max_index_length</th>
        <th>Temporary</th>
    </tr>
    <tr>
        <td>user</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>None</td>
        <td>VIEW</td>
        <td>None</td>
        <td>None</td>
    </tr>
</table>



## 5. mysql用户管理


```python
%%sql
use mysql;
create user test identified by 'test123';
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.
    0 rows affected.





    []




```python
%sql mysql+pymysql://test:test123@172.17.0.1:12306
```




    'Connected: test@None'




```python
%sql show databases;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
     * mysql+pymysql://test:***@172.17.0.1:12306
    1 rows affected.





<table>
    <tr>
        <th>Database</th>
    </tr>
    <tr>
        <td>information_schema</td>
    </tr>
</table>




```python
%sql use information_schema;show tables;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.
    77 rows affected.





<table>
    <tr>
        <th>Tables_in_information_schema</th>
    </tr>
    <tr>
        <td>ALL_PLUGINS</td>
    </tr>
    <tr>
        <td>APPLICABLE_ROLES</td>
    </tr>
    <tr>
        <td>CHARACTER_SETS</td>
    </tr>
    <tr>
        <td>CHECK_CONSTRAINTS</td>
    </tr>
    <tr>
        <td>COLLATIONS</td>
    </tr>
    <tr>
        <td>COLLATION_CHARACTER_SET_APPLICABILITY</td>
    </tr>
    <tr>
        <td>COLUMNS</td>
    </tr>
    <tr>
        <td>COLUMN_PRIVILEGES</td>
    </tr>
    <tr>
        <td>ENABLED_ROLES</td>
    </tr>
    <tr>
        <td>ENGINES</td>
    </tr>
    <tr>
        <td>EVENTS</td>
    </tr>
    <tr>
        <td>FILES</td>
    </tr>
    <tr>
        <td>GLOBAL_STATUS</td>
    </tr>
    <tr>
        <td>GLOBAL_VARIABLES</td>
    </tr>
    <tr>
        <td>KEY_CACHES</td>
    </tr>
    <tr>
        <td>KEY_COLUMN_USAGE</td>
    </tr>
    <tr>
        <td>OPTIMIZER_TRACE</td>
    </tr>
    <tr>
        <td>PARAMETERS</td>
    </tr>
    <tr>
        <td>PARTITIONS</td>
    </tr>
    <tr>
        <td>PLUGINS</td>
    </tr>
    <tr>
        <td>PROCESSLIST</td>
    </tr>
    <tr>
        <td>PROFILING</td>
    </tr>
    <tr>
        <td>REFERENTIAL_CONSTRAINTS</td>
    </tr>
    <tr>
        <td>ROUTINES</td>
    </tr>
    <tr>
        <td>SCHEMATA</td>
    </tr>
    <tr>
        <td>SCHEMA_PRIVILEGES</td>
    </tr>
    <tr>
        <td>SESSION_STATUS</td>
    </tr>
    <tr>
        <td>SESSION_VARIABLES</td>
    </tr>
    <tr>
        <td>STATISTICS</td>
    </tr>
    <tr>
        <td>SYSTEM_VARIABLES</td>
    </tr>
    <tr>
        <td>TABLES</td>
    </tr>
    <tr>
        <td>TABLESPACES</td>
    </tr>
    <tr>
        <td>TABLE_CONSTRAINTS</td>
    </tr>
    <tr>
        <td>TABLE_PRIVILEGES</td>
    </tr>
    <tr>
        <td>TRIGGERS</td>
    </tr>
    <tr>
        <td>USER_PRIVILEGES</td>
    </tr>
    <tr>
        <td>VIEWS</td>
    </tr>
    <tr>
        <td>GEOMETRY_COLUMNS</td>
    </tr>
    <tr>
        <td>SPATIAL_REF_SYS</td>
    </tr>
    <tr>
        <td>CLIENT_STATISTICS</td>
    </tr>
    <tr>
        <td>INDEX_STATISTICS</td>
    </tr>
    <tr>
        <td>INNODB_SYS_DATAFILES</td>
    </tr>
    <tr>
        <td>USER_STATISTICS</td>
    </tr>
    <tr>
        <td>INNODB_SYS_TABLESTATS</td>
    </tr>
    <tr>
        <td>INNODB_LOCKS</td>
    </tr>
    <tr>
        <td>INNODB_MUTEXES</td>
    </tr>
    <tr>
        <td>INNODB_CMPMEM</td>
    </tr>
    <tr>
        <td>INNODB_CMP_PER_INDEX</td>
    </tr>
    <tr>
        <td>INNODB_CMP</td>
    </tr>
    <tr>
        <td>INNODB_FT_DELETED</td>
    </tr>
    <tr>
        <td>INNODB_CMP_RESET</td>
    </tr>
    <tr>
        <td>INNODB_LOCK_WAITS</td>
    </tr>
    <tr>
        <td>TABLE_STATISTICS</td>
    </tr>
    <tr>
        <td>INNODB_TABLESPACES_ENCRYPTION</td>
    </tr>
    <tr>
        <td>INNODB_BUFFER_PAGE_LRU</td>
    </tr>
    <tr>
        <td>INNODB_SYS_FIELDS</td>
    </tr>
    <tr>
        <td>INNODB_CMPMEM_RESET</td>
    </tr>
    <tr>
        <td>INNODB_SYS_COLUMNS</td>
    </tr>
    <tr>
        <td>INNODB_FT_INDEX_TABLE</td>
    </tr>
    <tr>
        <td>INNODB_CMP_PER_INDEX_RESET</td>
    </tr>
    <tr>
        <td>user_variables</td>
    </tr>
    <tr>
        <td>INNODB_FT_INDEX_CACHE</td>
    </tr>
    <tr>
        <td>INNODB_SYS_FOREIGN_COLS</td>
    </tr>
    <tr>
        <td>INNODB_FT_BEING_DELETED</td>
    </tr>
    <tr>
        <td>INNODB_BUFFER_POOL_STATS</td>
    </tr>
    <tr>
        <td>INNODB_TRX</td>
    </tr>
    <tr>
        <td>INNODB_SYS_FOREIGN</td>
    </tr>
    <tr>
        <td>INNODB_SYS_TABLES</td>
    </tr>
    <tr>
        <td>INNODB_FT_DEFAULT_STOPWORD</td>
    </tr>
    <tr>
        <td>INNODB_FT_CONFIG</td>
    </tr>
    <tr>
        <td>INNODB_BUFFER_PAGE</td>
    </tr>
    <tr>
        <td>INNODB_SYS_TABLESPACES</td>
    </tr>
    <tr>
        <td>INNODB_METRICS</td>
    </tr>
    <tr>
        <td>INNODB_SYS_INDEXES</td>
    </tr>
    <tr>
        <td>INNODB_SYS_VIRTUAL</td>
    </tr>
    <tr>
        <td>INNODB_TABLESPACES_SCRUBBING</td>
    </tr>
    <tr>
        <td>INNODB_SYS_SEMAPHORE_WAITS</td>
    </tr>
</table>




```python
%sql mysql+pymysql://root:********@172.17.0.1:12306/mysql
```




    'Connected: root@mysql'




```python
%sql select * from user;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
       mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    3 rows affected.





<table>
    <tr>
        <th>Host</th>
        <th>User</th>
        <th>Password</th>
        <th>Select_priv</th>
        <th>Insert_priv</th>
        <th>Update_priv</th>
        <th>Delete_priv</th>
        <th>Create_priv</th>
        <th>Drop_priv</th>
        <th>Reload_priv</th>
        <th>Shutdown_priv</th>
        <th>Process_priv</th>
        <th>File_priv</th>
        <th>Grant_priv</th>
        <th>References_priv</th>
        <th>Index_priv</th>
        <th>Alter_priv</th>
        <th>Show_db_priv</th>
        <th>Super_priv</th>
        <th>Create_tmp_table_priv</th>
        <th>Lock_tables_priv</th>
        <th>Execute_priv</th>
        <th>Repl_slave_priv</th>
        <th>Repl_client_priv</th>
        <th>Create_view_priv</th>
        <th>Show_view_priv</th>
        <th>Create_routine_priv</th>
        <th>Alter_routine_priv</th>
        <th>Create_user_priv</th>
        <th>Event_priv</th>
        <th>Trigger_priv</th>
        <th>Create_tablespace_priv</th>
        <th>Delete_history_priv</th>
        <th>ssl_type</th>
        <th>ssl_cipher</th>
        <th>x509_issuer</th>
        <th>x509_subject</th>
        <th>max_questions</th>
        <th>max_updates</th>
        <th>max_connections</th>
        <th>max_user_connections</th>
        <th>plugin</th>
        <th>authentication_string</th>
        <th>password_expired</th>
        <th>is_role</th>
        <th>default_role</th>
        <th>max_statement_time</th>
    </tr>
    <tr>
        <td>localhost</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>tjc</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
</table>




```python
%sql drop user test;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.





    []




```python
%sql select * from user;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    2 rows affected.





<table>
    <tr>
        <th>Host</th>
        <th>User</th>
        <th>Password</th>
        <th>Select_priv</th>
        <th>Insert_priv</th>
        <th>Update_priv</th>
        <th>Delete_priv</th>
        <th>Create_priv</th>
        <th>Drop_priv</th>
        <th>Reload_priv</th>
        <th>Shutdown_priv</th>
        <th>Process_priv</th>
        <th>File_priv</th>
        <th>Grant_priv</th>
        <th>References_priv</th>
        <th>Index_priv</th>
        <th>Alter_priv</th>
        <th>Show_db_priv</th>
        <th>Super_priv</th>
        <th>Create_tmp_table_priv</th>
        <th>Lock_tables_priv</th>
        <th>Execute_priv</th>
        <th>Repl_slave_priv</th>
        <th>Repl_client_priv</th>
        <th>Create_view_priv</th>
        <th>Show_view_priv</th>
        <th>Create_routine_priv</th>
        <th>Alter_routine_priv</th>
        <th>Create_user_priv</th>
        <th>Event_priv</th>
        <th>Trigger_priv</th>
        <th>Create_tablespace_priv</th>
        <th>Delete_history_priv</th>
        <th>ssl_type</th>
        <th>ssl_cipher</th>
        <th>x509_issuer</th>
        <th>x509_subject</th>
        <th>max_questions</th>
        <th>max_updates</th>
        <th>max_connections</th>
        <th>max_user_connections</th>
        <th>plugin</th>
        <th>authentication_string</th>
        <th>password_expired</th>
        <th>is_role</th>
        <th>default_role</th>
        <th>max_statement_time</th>
    </tr>
    <tr>
        <td>localhost</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
</table>



* 刷新权限


```python
%sql FLUSH PRIVILEGES;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.





    []



## 6. 创建和删除数据库 


```python
%sql mysql+pymysql://root:********@172.17.0.1:12306
```




    'Connected: root@None'




```python
%%sql
create database testdb;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    1 rows affected.





    []




```python
%%sql
#drop database testdb;
drop database tjcdb;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.
    0 rows affected.





    []




```python
%sql flush privileges
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    0 rows affected.





    []




```python
#如果数据库存在就不创建，不存在就创建，并将字符集设置为utf8
%sql CREATE DATABASE IF NOT EXISTS tjcdb DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    1 rows affected.





    []



* 创建对应数据库用户，并授予全部权限


```python
%%sql
use tjcdb;
grant all privileges on tjcdb.* to tjc identified by '********';
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
     * mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
       mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.
    0 rows affected.





    []




```python
%sql select * from mysql.user;
```

     * mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
    3 rows affected.





<table>
    <tr>
        <th>Host</th>
        <th>User</th>
        <th>Password</th>
        <th>Select_priv</th>
        <th>Insert_priv</th>
        <th>Update_priv</th>
        <th>Delete_priv</th>
        <th>Create_priv</th>
        <th>Drop_priv</th>
        <th>Reload_priv</th>
        <th>Shutdown_priv</th>
        <th>Process_priv</th>
        <th>File_priv</th>
        <th>Grant_priv</th>
        <th>References_priv</th>
        <th>Index_priv</th>
        <th>Alter_priv</th>
        <th>Show_db_priv</th>
        <th>Super_priv</th>
        <th>Create_tmp_table_priv</th>
        <th>Lock_tables_priv</th>
        <th>Execute_priv</th>
        <th>Repl_slave_priv</th>
        <th>Repl_client_priv</th>
        <th>Create_view_priv</th>
        <th>Show_view_priv</th>
        <th>Create_routine_priv</th>
        <th>Alter_routine_priv</th>
        <th>Create_user_priv</th>
        <th>Event_priv</th>
        <th>Trigger_priv</th>
        <th>Create_tablespace_priv</th>
        <th>Delete_history_priv</th>
        <th>ssl_type</th>
        <th>ssl_cipher</th>
        <th>x509_issuer</th>
        <th>x509_subject</th>
        <th>max_questions</th>
        <th>max_updates</th>
        <th>max_connections</th>
        <th>max_user_connections</th>
        <th>plugin</th>
        <th>authentication_string</th>
        <th>password_expired</th>
        <th>is_role</th>
        <th>default_role</th>
        <th>max_statement_time</th>
    </tr>
    <tr>
        <td>localhost</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>tjc</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
</table>




```python
%sql mysql+pymysql://tjc:********@172.17.0.1:12306/tjcdb
```




    'Connected: tjc@tjcdb'



## 7.  创建管理数据库表


```python
%%sql
create table if not exists `memberinfo`(
    `memberid` int unsigned auto_increment comment '自动编号',
    `membername` varchar(10) not null comment '姓名',
    `gender` char(1) not null comment '性别',
    `birthday` date  comment '出生年月日',
    `address` varchar(100) not null comment '家庭住址',
    `latitude` float(12,9) null comment '纬度',
    `longitude` float(12,9) null comment '经度',
    `phone` varchar(20) not null comment '电话',
    `baptism` char(1) not null comment '水洗，Y或N',
`spirit` char(1) not null comment '灵洗,Y或N',
`group` varchar(10) not null comment '组别',
`area` varchar(10) not null comment '片区 ',
`church` varchar(10) not null comment '所属堂点 ',
`health` varchar(10) not null comment '身体状态：正常，无法出门，已故 ',
`fatherid` int(10) not null comment '父亲编号 ',
`motherid` int(10) not null comment '母亲编号 ',
`remarks` varchar(200) not null comment '备注 ',
    primary key(memberid)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%%sql
show tables;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>Tables_in_tjcdb</th>
    </tr>
    <tr>
        <td>memberinfo</td>
    </tr>
</table>




```python
%sql show table status from tjcdb
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>Name</th>
        <th>Engine</th>
        <th>Version</th>
        <th>Row_format</th>
        <th>Rows</th>
        <th>Avg_row_length</th>
        <th>Data_length</th>
        <th>Max_data_length</th>
        <th>Index_length</th>
        <th>Data_free</th>
        <th>Auto_increment</th>
        <th>Create_time</th>
        <th>Update_time</th>
        <th>Check_time</th>
        <th>Collation</th>
        <th>Checksum</th>
        <th>Create_options</th>
        <th>Comment</th>
        <th>Max_index_length</th>
        <th>Temporary</th>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>InnoDB</td>
        <td>10</td>
        <td>Dynamic</td>
        <td>0</td>
        <td>0</td>
        <td>16384</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>2020-03-11 09:20:15</td>
        <td>None</td>
        <td>None</td>
        <td>utf8_general_ci</td>
        <td>None</td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>N</td>
    </tr>
</table>




```python
%sql desc memberinfo
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    17 rows affected.





<table>
    <tr>
        <th>Field</th>
        <th>Type</th>
        <th>Null</th>
        <th>Key</th>
        <th>Default</th>
        <th>Extra</th>
    </tr>
    <tr>
        <td>memberid</td>
        <td>int(10) unsigned</td>
        <td>NO</td>
        <td>PRI</td>
        <td>None</td>
        <td>auto_increment</td>
    </tr>
    <tr>
        <td>membername</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>gender</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>birthday</td>
        <td>date</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>address</td>
        <td>varchar(100)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>latitude</td>
        <td>float(12,9)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>longitude</td>
        <td>float(12,9)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>phone</td>
        <td>varchar(20)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>baptism</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>spirit</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>membergroup</td>
        <td>varchar(10)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>area</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>church</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>health</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>fatherid</td>
        <td>int(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>motherid</td>
        <td>int(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>remarks</td>
        <td>varchar(200)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
</table>



* 修改表


```python
%%sql
alter table memberinfo change column `group` membergroup varchar(10)
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []



## 8. 数据的插入、删除、更新、查询、条件查询 


```python
%sql mysql+pymysql://tjc:********@172.17.0.1:12306/tjcdb
```




    'Connected: tjc@tjcdb'



* 插入


```python
%%sql
insert into memberinfo (membername,gender,birthday,address,phone,baptism,spirit,membergroup,area,church,health,fatherid,motherid,remarks) 
values('何以勒','m','1983-12-20','厦门市思明区罗宾森广场一期琥珀阁2207室','13959248164','Y','Y','三组','火车站','厦港堂','正常',0,0,'')
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb



    ---------------------------------------------------------------------------
    
    IntegrityError                            Traceback (most recent call last)
    
    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in _execute_context(self, dialect, constructor, statement, parameters, *args)
       1245                     self.dialect.do_execute(
    -> 1246                         cursor, statement, parameters, context
       1247                     )


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/default.py in do_execute(self, cursor, statement, parameters, context)
        580     def do_execute(self, cursor, statement, parameters, context=None):
    --> 581         cursor.execute(statement, parameters)
        582 


    /opt/conda/lib/python3.7/site-packages/pymysql/cursors.py in execute(self, query, args)
        169 
    --> 170         result = self._query(query)
        171         self._executed = query


    /opt/conda/lib/python3.7/site-packages/pymysql/cursors.py in _query(self, q)
        327         self._clear_result()
    --> 328         conn.query(q)
        329         self._do_get_result()


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in query(self, sql, unbuffered)
        516         self._execute_command(COMMAND.COM_QUERY, sql)
    --> 517         self._affected_rows = self._read_query_result(unbuffered=unbuffered)
        518         return self._affected_rows


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in _read_query_result(self, unbuffered)
        731             result = MySQLResult(self)
    --> 732             result.read()
        733         self._result = result


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in read(self)
       1074         try:
    -> 1075             first_packet = self.connection._read_packet()
       1076 


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in _read_packet(self, packet_type)
        683         packet = packet_type(buff, self.encoding)
    --> 684         packet.check_error()
        685         return packet


    /opt/conda/lib/python3.7/site-packages/pymysql/protocol.py in check_error(self)
        219             if DEBUG: print("errno =", errno)
    --> 220             err.raise_mysql_exception(self._data)
        221 


    /opt/conda/lib/python3.7/site-packages/pymysql/err.py in raise_mysql_exception(data)
        108     errorclass = error_map.get(errno, InternalError)
    --> 109     raise errorclass(errno, errval)


    IntegrityError: (1062, "Duplicate entry '何以勒-厦门市思明区罗宾森广场一期琥珀阁2207' for key 'idx_member'")


​    
    The above exception was the direct cause of the following exception:


    IntegrityError                            Traceback (most recent call last)
    
    <ipython-input-203-69d7c965a6c3> in <module>
    ----> 1 get_ipython().run_cell_magic('sql', '', "insert into memberinfo (membername,gender,birthday,address,phone,baptism,spirit,membergroup,area,church,health,fatherid,motherid,remarks) \nvalues('何以勒','m','1983-12-20','厦门市思明区罗宾森广场一期琥珀阁2207室','13959248164','Y','Y','三组','火车站','厦港堂','正常',0,0,'')\n")


    /opt/conda/lib/python3.7/site-packages/IPython/core/interactiveshell.py in run_cell_magic(self, magic_name, line, cell)
       2350             with self.builtin_trap:
       2351                 args = (magic_arg_s, cell)
    -> 2352                 result = fn(*args, **kwargs)
       2353             return result
       2354 


    </opt/conda/lib/python3.7/site-packages/decorator.py:decorator-gen-157> in execute(self, line, cell, local_ns)


    /opt/conda/lib/python3.7/site-packages/IPython/core/magic.py in <lambda>(f, *a, **k)
        185     # but it's overkill for just that one bit of state.
        186     def magic_deco(arg):
    --> 187         call = lambda f, *a, **k: f(*a, **k)
        188 
        189         if callable(arg):


    </opt/conda/lib/python3.7/site-packages/decorator.py:decorator-gen-156> in execute(self, line, cell, local_ns)


    /opt/conda/lib/python3.7/site-packages/IPython/core/magic.py in <lambda>(f, *a, **k)
        185     # but it's overkill for just that one bit of state.
        186     def magic_deco(arg):
    --> 187         call = lambda f, *a, **k: f(*a, **k)
        188 
        189         if callable(arg):


    /opt/conda/lib/python3.7/site-packages/sql/magic.py in execute(self, line, cell, local_ns)
         93 
         94         try:
    ---> 95             result = sql.run.run(conn, parsed['sql'], self, user_ns)
         96 
         97             if result is not None and not isinstance(result, str) and self.column_local_vars:


    /opt/conda/lib/python3.7/site-packages/sql/run.py in run(conn, sql, config, user_namespace)
        338             else:
        339                 txt = sqlalchemy.sql.text(statement)
    --> 340                 result = conn.session.execute(txt, user_namespace)
        341             _commit(conn=conn, config=config)
        342             if result and config.feedback:


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in execute(self, object_, *multiparams, **params)
        980             raise exc.ObjectNotExecutableError(object_)
        981         else:
    --> 982             return meth(self, multiparams, params)
        983 
        984     def _execute_function(self, func, multiparams, params):


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/sql/elements.py in _execute_on_connection(self, connection, multiparams, params)
        285     def _execute_on_connection(self, connection, multiparams, params):
        286         if self.supports_execution:
    --> 287             return connection._execute_clauseelement(self, multiparams, params)
        288         else:
        289             raise exc.ObjectNotExecutableError(self)


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in _execute_clauseelement(self, elem, multiparams, params)
       1099             distilled_params,
       1100             compiled_sql,
    -> 1101             distilled_params,
       1102         )
       1103         if self._has_events or self.engine._has_events:


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in _execute_context(self, dialect, constructor, statement, parameters, *args)
       1248         except BaseException as e:
       1249             self._handle_dbapi_exception(
    -> 1250                 e, statement, parameters, cursor, context
       1251             )
       1252 


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in _handle_dbapi_exception(self, e, statement, parameters, cursor, context)
       1474                 util.raise_from_cause(newraise, exc_info)
       1475             elif should_wrap:
    -> 1476                 util.raise_from_cause(sqlalchemy_exception, exc_info)
       1477             else:
       1478                 util.reraise(*exc_info)


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/util/compat.py in raise_from_cause(exception, exc_info)
        396     exc_type, exc_value, exc_tb = exc_info
        397     cause = exc_value if exc_value is not exception else None
    --> 398     reraise(type(exception), exception, tb=exc_tb, cause=cause)
        399 
        400 


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/util/compat.py in reraise(tp, value, tb, cause)
        150             value.__cause__ = cause
        151         if value.__traceback__ is not tb:
    --> 152             raise value.with_traceback(tb)
        153         raise value
        154 


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/base.py in _execute_context(self, dialect, constructor, statement, parameters, *args)
       1244                 if not evt_handled:
       1245                     self.dialect.do_execute(
    -> 1246                         cursor, statement, parameters, context
       1247                     )
       1248         except BaseException as e:


    /opt/conda/lib/python3.7/site-packages/sqlalchemy/engine/default.py in do_execute(self, cursor, statement, parameters, context)
        579 
        580     def do_execute(self, cursor, statement, parameters, context=None):
    --> 581         cursor.execute(statement, parameters)
        582 
        583     def do_execute_no_params(self, cursor, statement, context=None):


    /opt/conda/lib/python3.7/site-packages/pymysql/cursors.py in execute(self, query, args)
        168         query = self.mogrify(query, args)
        169 
    --> 170         result = self._query(query)
        171         self._executed = query
        172         return result


    /opt/conda/lib/python3.7/site-packages/pymysql/cursors.py in _query(self, q)
        326         self._last_executed = q
        327         self._clear_result()
    --> 328         conn.query(q)
        329         self._do_get_result()
        330         return self.rowcount


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in query(self, sql, unbuffered)
        515                 sql = sql.encode(self.encoding, 'surrogateescape')
        516         self._execute_command(COMMAND.COM_QUERY, sql)
    --> 517         self._affected_rows = self._read_query_result(unbuffered=unbuffered)
        518         return self._affected_rows
        519 


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in _read_query_result(self, unbuffered)
        730         else:
        731             result = MySQLResult(self)
    --> 732             result.read()
        733         self._result = result
        734         if result.server_status is not None:


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in read(self)
       1073     def read(self):
       1074         try:
    -> 1075             first_packet = self.connection._read_packet()
       1076 
       1077             if first_packet.is_ok_packet():


    /opt/conda/lib/python3.7/site-packages/pymysql/connections.py in _read_packet(self, packet_type)
        682 
        683         packet = packet_type(buff, self.encoding)
    --> 684         packet.check_error()
        685         return packet
        686 


    /opt/conda/lib/python3.7/site-packages/pymysql/protocol.py in check_error(self)
        218             errno = self.read_uint16()
        219             if DEBUG: print("errno =", errno)
    --> 220             err.raise_mysql_exception(self._data)
        221 
        222     def dump(self):


    /opt/conda/lib/python3.7/site-packages/pymysql/err.py in raise_mysql_exception(data)
        107         errval = data[3:].decode('utf-8', 'replace')
        108     errorclass = error_map.get(errno, InternalError)
    --> 109     raise errorclass(errno, errval)


    IntegrityError: (pymysql.err.IntegrityError) (1062, "Duplicate entry '何以勒-厦门市思明区罗宾森广场一期琥珀阁2207' for key 'idx_member'")
    [SQL: insert into memberinfo (membername,gender,birthday,address,phone,baptism,spirit,membergroup,area,church,health,fatherid,motherid,remarks) 
    values('何以勒','m','1983-12-20','厦门市思明区罗宾森广场一期琥珀阁2207室','13959248164','Y','Y','三组','火车站','厦港堂','正常',0,0,'')]
    (Background on this error at: http://sqlalche.me/e/gkpj)



```python
%sql select * from memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>memberid</th>
        <th>membername</th>
        <th>gender</th>
        <th>birthday</th>
        <th>address</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>phone</th>
        <th>baptism</th>
        <th>spirit</th>
        <th>membergroup</th>
        <th>area</th>
        <th>church</th>
        <th>health</th>
        <th>fatherid</th>
        <th>motherid</th>
        <th>remarks</th>
    </tr>
    <tr>
        <td>1</td>
        <td>何以勒</td>
        <td>m</td>
        <td>1983-12-20</td>
        <td>厦门市思明区罗宾森广场一期琥珀阁2207室</td>
        <td>None</td>
        <td>None</td>
        <td>13959248164</td>
        <td>Y</td>
        <td>Y</td>
        <td>三组</td>
        <td>火车站</td>
        <td>厦港堂</td>
        <td>正常</td>
        <td>0</td>
        <td>0</td>
        <td></td>
    </tr>
</table>




```python
%sql update memberinfo set membergroup='中坚三组' where memberid=1;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





    []




```python
%sql select * from memberinfo where membername='何以勒'
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>memberid</th>
        <th>membername</th>
        <th>gender</th>
        <th>birthday</th>
        <th>address</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>phone</th>
        <th>baptism</th>
        <th>spirit</th>
        <th>membergroup</th>
        <th>area</th>
        <th>church</th>
        <th>health</th>
        <th>fatherid</th>
        <th>motherid</th>
        <th>remarks</th>
    </tr>
    <tr>
        <td>1</td>
        <td>何以勒</td>
        <td>m</td>
        <td>1983-12-20</td>
        <td>厦门市思明区罗宾森广场一期琥珀阁2207室</td>
        <td>None</td>
        <td>None</td>
        <td>13959248164</td>
        <td>Y</td>
        <td>Y</td>
        <td>中坚三组</td>
        <td>火车站</td>
        <td>厦港堂</td>
        <td>正常</td>
        <td>0</td>
        <td>0</td>
        <td></td>
    </tr>
</table>



* 正则查询


```python
%sql select * from memberinfo where phone regexp '[^7]'
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>memberid</th>
        <th>membername</th>
        <th>gender</th>
        <th>birthday</th>
        <th>address</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>phone</th>
        <th>baptism</th>
        <th>spirit</th>
        <th>membergroup</th>
        <th>area</th>
        <th>church</th>
        <th>health</th>
        <th>fatherid</th>
        <th>motherid</th>
        <th>remarks</th>
    </tr>
    <tr>
        <td>1</td>
        <td>何以勒</td>
        <td>m</td>
        <td>1983-12-20</td>
        <td>厦门市思明区罗宾森广场一期琥珀阁2207室</td>
        <td>0.0</td>
        <td>0.0</td>
        <td>13959248164</td>
        <td>Y</td>
        <td>Y</td>
        <td>中坚三组</td>
        <td>火车站</td>
        <td>厦港堂</td>
        <td>正常</td>
        <td>0</td>
        <td>0</td>
        <td></td>
    </tr>
</table>



## 9. Alter 修改操作 

* 修改表名


```python
%sql alter table memberinfo rename to memberinfo_bak;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%sql show tables;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>Tables_in_tjcdb</th>
    </tr>
    <tr>
        <td>memberinfo_bak</td>
    </tr>
</table>




```python
%sql rename table memberinfo_bak to memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%sql show tables
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>Tables_in_tjcdb</th>
    </tr>
    <tr>
        <td>memberinfo</td>
    </tr>
</table>




```python
%sql desc memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    17 rows affected.





<table>
    <tr>
        <th>Field</th>
        <th>Type</th>
        <th>Null</th>
        <th>Key</th>
        <th>Default</th>
        <th>Extra</th>
    </tr>
    <tr>
        <td>memberid</td>
        <td>int(10) unsigned</td>
        <td>NO</td>
        <td>PRI</td>
        <td>None</td>
        <td>auto_increment</td>
    </tr>
    <tr>
        <td>membername</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>gender</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>birthday</td>
        <td>date</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>address</td>
        <td>varchar(100)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>latitude</td>
        <td>float(12,9)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>longitude</td>
        <td>float(12,9)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>phone</td>
        <td>varchar(20)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>baptism</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>spirit</td>
        <td>char(1)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>membergroup</td>
        <td>varchar(10)</td>
        <td>YES</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>area</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>church</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>health</td>
        <td>varchar(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>fatherid</td>
        <td>int(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>motherid</td>
        <td>int(10)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
    <tr>
        <td>remarks</td>
        <td>varchar(200)</td>
        <td>NO</td>
        <td></td>
        <td>None</td>
        <td></td>
    </tr>
</table>



* 修改字段属性


```python
%%sql 
update memberinfo set latitude=0,longitude=0 where 1=1;
alter table memberinfo modify latitude float(12,9) not null default 0;
alter table memberinfo modify longitude float(12,9) not null default 0;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.
    0 rows affected.
    0 rows affected.





    []




```python
%sql select * from memberinfo
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>memberid</th>
        <th>membername</th>
        <th>gender</th>
        <th>birthday</th>
        <th>address</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>phone</th>
        <th>baptism</th>
        <th>spirit</th>
        <th>membergroup</th>
        <th>area</th>
        <th>church</th>
        <th>health</th>
        <th>fatherid</th>
        <th>motherid</th>
        <th>remarks</th>
    </tr>
    <tr>
        <td>1</td>
        <td>何以勒</td>
        <td>m</td>
        <td>1983-12-20</td>
        <td>厦门市思明区罗宾森广场一期琥珀阁2207室</td>
        <td>0.0</td>
        <td>0.0</td>
        <td>13959248164</td>
        <td>Y</td>
        <td>Y</td>
        <td>中坚三组</td>
        <td>火车站</td>
        <td>厦港堂</td>
        <td>正常</td>
        <td>0</td>
        <td>0</td>
        <td></td>
    </tr>
</table>



## 10. 创建索引 


```python
%sql create unique index idx_member on memberinfo(membername,address)
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%sql create index idx_phone on memberinfo(phone)
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%sql show index from memberinfo
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    4 rows affected.





<table>
    <tr>
        <th>Table</th>
        <th>Non_unique</th>
        <th>Key_name</th>
        <th>Seq_in_index</th>
        <th>Column_name</th>
        <th>Collation</th>
        <th>Cardinality</th>
        <th>Sub_part</th>
        <th>Packed</th>
        <th>Null</th>
        <th>Index_type</th>
        <th>Comment</th>
        <th>Index_comment</th>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>0</td>
        <td>PRIMARY</td>
        <td>1</td>
        <td>memberid</td>
        <td>A</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td></td>
        <td>BTREE</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>0</td>
        <td>idx_member</td>
        <td>1</td>
        <td>membername</td>
        <td>A</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td></td>
        <td>BTREE</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>0</td>
        <td>idx_member</td>
        <td>2</td>
        <td>address</td>
        <td>A</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td></td>
        <td>BTREE</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>1</td>
        <td>idx_phone</td>
        <td>1</td>
        <td>phone</td>
        <td>A</td>
        <td>0</td>
        <td>None</td>
        <td>None</td>
        <td></td>
        <td>BTREE</td>
        <td></td>
        <td></td>
    </tr>
</table>



## 11. 复制表 


```python
%sql show create table memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>Table</th>
        <th>Create Table</th>
    </tr>
    <tr>
        <td>memberinfo</td>
        <td>CREATE TABLE `memberinfo` (<br>  `memberid` int(10) unsigned NOT NULL AUTO_INCREMENT COMMENT &#x27;自动编号&#x27;,<br>  `membername` varchar(10) NOT NULL COMMENT &#x27;姓名&#x27;,<br>  `gender` char(1) NOT NULL COMMENT &#x27;性别&#x27;,<br>  `birthday` date DEFAULT NULL COMMENT &#x27;出生年月日&#x27;,<br>  `address` varchar(100) NOT NULL COMMENT &#x27;家庭住址&#x27;,<br>  `latitude` float(12,9) NOT NULL DEFAULT 0.000000000,<br>  `longitude` float(12,9) NOT NULL DEFAULT 0.000000000,<br>  `phone` varchar(20) NOT NULL COMMENT &#x27;电话&#x27;,<br>  `baptism` char(1) NOT NULL COMMENT &#x27;水洗，Y或N&#x27;,<br>  `spirit` char(1) NOT NULL COMMENT &#x27;灵洗,Y或N&#x27;,<br>  `membergroup` varchar(10) DEFAULT NULL,<br>  `area` varchar(10) NOT NULL COMMENT &#x27;片区 &#x27;,<br>  `church` varchar(10) NOT NULL COMMENT &#x27;所属堂点 &#x27;,<br>  `health` varchar(10) NOT NULL COMMENT &#x27;身体状态：正常，无法出门，已故 &#x27;,<br>  `fatherid` int(10) NOT NULL COMMENT &#x27;父亲编号 &#x27;,<br>  `motherid` int(10) NOT NULL COMMENT &#x27;母亲编号 &#x27;,<br>  `remarks` varchar(200) NOT NULL COMMENT &#x27;备注 &#x27;,<br>  PRIMARY KEY (`memberid`),<br>  UNIQUE KEY `idx_member` (`membername`,`address`),<br>  KEY `idx_phone` (`phone`)<br>) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8</td>
    </tr>
</table>



## 12. MySql元数据 


```python
#服务器版本信息
%sql select version()
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>version()</th>
    </tr>
    <tr>
        <td>10.4.8-MariaDB-1:10.4.8+maria~bionic</td>
    </tr>
</table>




```python
#当前数据库名
%sql select database()
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>database()</th>
    </tr>
    <tr>
        <td>tjcdb</td>
    </tr>
</table>




```python
%sql select user();
#%sql show status;
#%sql show variables;

```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>user()</th>
    </tr>
    <tr>
        <td>tjc@172.17.0.1</td>
    </tr>
</table>



## 13. 数据导入、导出 

* 数据导出


```python
%sql mysql+pymysql://tjc:********@172.17.0.1:12306/tjcdb
```




    'Connected: tjc@tjcdb'




```python
%%sql
select *  into outfile 'memberinfo.txt'
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\n'
from memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://root:***@172.17.0.1:12306/tjcdb
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.




```python
%%sql 
mysql+pymysql://root:********@172.17.0.1:12306/tjcdb
select * from mysql.user;
```

    3 rows affected.





<table>
    <tr>
        <th>Host</th>
        <th>User</th>
        <th>Password</th>
        <th>Select_priv</th>
        <th>Insert_priv</th>
        <th>Update_priv</th>
        <th>Delete_priv</th>
        <th>Create_priv</th>
        <th>Drop_priv</th>
        <th>Reload_priv</th>
        <th>Shutdown_priv</th>
        <th>Process_priv</th>
        <th>File_priv</th>
        <th>Grant_priv</th>
        <th>References_priv</th>
        <th>Index_priv</th>
        <th>Alter_priv</th>
        <th>Show_db_priv</th>
        <th>Super_priv</th>
        <th>Create_tmp_table_priv</th>
        <th>Lock_tables_priv</th>
        <th>Execute_priv</th>
        <th>Repl_slave_priv</th>
        <th>Repl_client_priv</th>
        <th>Create_view_priv</th>
        <th>Show_view_priv</th>
        <th>Create_routine_priv</th>
        <th>Alter_routine_priv</th>
        <th>Create_user_priv</th>
        <th>Event_priv</th>
        <th>Trigger_priv</th>
        <th>Create_tablespace_priv</th>
        <th>Delete_history_priv</th>
        <th>ssl_type</th>
        <th>ssl_cipher</th>
        <th>x509_issuer</th>
        <th>x509_subject</th>
        <th>max_questions</th>
        <th>max_updates</th>
        <th>max_connections</th>
        <th>max_user_connections</th>
        <th>plugin</th>
        <th>authentication_string</th>
        <th>password_expired</th>
        <th>is_role</th>
        <th>default_role</th>
        <th>max_statement_time</th>
    </tr>
    <tr>
        <td>localhost</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>root</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td>Y</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*F2C8A97A21E42B3735A4C88136E139460F40B4FC</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
    <tr>
        <td>%</td>
        <td>tjc</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>Y</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td></td>
        <td></td>
        <td></td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>mysql_native_password</td>
        <td>*28F13C854B563783661E6DC37017E94C41CBC595</td>
        <td>N</td>
        <td>N</td>
        <td></td>
        <td>0.000000</td>
    </tr>
</table>




```python
%sql grant file on *.* to tjc;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
     * mysql+pymysql://root:***@172.17.0.1:12306/tjcdb
       mysql+pymysql://test:***@172.17.0.1:12306
       mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```bash
%%bash 
mysqldump -utjc -h 172.17.0.1 -P 12306 -p******** tjcdb >tjcdb.dmp
```

    mysqldump: [Warning] Using a password on the command line interface can be insecure.


* 数据导入


```python
%sql truncate table memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
     * mysql+pymysql://root:***@172.17.0.1:12306/tjcdb
       mysql+pymysql://test:***@172.17.0.1:12306
       mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    0 rows affected.





    []




```python
%sql select * from memberinfo;
```

       mysql+pymysql://root:***@172.17.0.1:12306
       mysql+pymysql://root:***@172.17.0.1:12306/
       mysql+pymysql://root:***@172.17.0.1:12306/mysql
       mysql+pymysql://root:***@172.17.0.1:12306/tjcdb
       mysql+pymysql://test:***@172.17.0.1:12306
     * mysql+pymysql://tjc:***@172.17.0.1:12306/tjcdb
    1 rows affected.





<table>
    <tr>
        <th>memberid</th>
        <th>membername</th>
        <th>gender</th>
        <th>birthday</th>
        <th>address</th>
        <th>latitude</th>
        <th>longitude</th>
        <th>phone</th>
        <th>baptism</th>
        <th>spirit</th>
        <th>membergroup</th>
        <th>area</th>
        <th>church</th>
        <th>health</th>
        <th>fatherid</th>
        <th>motherid</th>
        <th>remarks</th>
    </tr>
    <tr>
        <td>1</td>
        <td>何以勒</td>
        <td>m</td>
        <td>1983-12-20</td>
        <td>厦门市思明区罗宾森广场一期琥珀阁2207室</td>
        <td>0.0</td>
        <td>0.0</td>
        <td>13959248164</td>
        <td>Y</td>
        <td>Y</td>
        <td>中坚三组</td>
        <td>火车站</td>
        <td>厦港堂</td>
        <td>正常</td>
        <td>0</td>
        <td>0</td>
        <td></td>
    </tr>
</table>




```bash
%%bash
mysqlimport -utjc -p******** -h 172.17.0.1 -P 12306 -r --local --fields-enclosed-by='"' --fields-terminated-by="," \
   --lines-terminated-by="\n" tjcdb memberinfo.txt
#mysqlimport|grep -i table
```

    tjcdb.memberinfo: Records: 1  Deleted: 1  Skipped: 0  Warnings: 0


    mysqlimport: [Warning] Using a password on the command line interface can be insecure.


## 14. Mysql函数（略）

[详见](https://www.runoob.com/mysql/mysql-functions.html)

