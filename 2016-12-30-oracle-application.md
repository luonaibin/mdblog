---
layout:     post
title:      "Oracle SQL常用"
date:       2016-12-30
---

<style type="text/css">
p{
	text-indent: 2em;
}
.post img {
  margin-bottom: 0rem;
}
</style>

###新建表create as select
-create table USERINFO as select * from OP_USERINFO;

###创建DBLink
-create database link prod_dblink connect to XXX_read identified by XXX_read using '(DESCRIPTION=(ADDRESS_LIST=(ADDRESS=(PROTOCOL=TCP)(HOST=127.0.1.11)(PORT=1521)))(CONNECT_DATA=(SERVICE_NAME=XXX)))';

###查询新建表或修改表的sql
-select a.LAST_ANALYZED, a.*, b.* from user_tables a, user_tab_comments b WHERE a.TABLE_NAME = b.TABLE_NAME order by a.LAST_ANALYZED desc

###查看当前用户的缺省表空间
-select username,default_tablespace from user_users;

###查看用户下所有的表
-select * from user_tables;

###查看AA表的主键约束名称，以及主键约束的字段名称。如果没有，则返回空
-select a.constraint_name,  a.column_name from user_cons_columns a, user_constraints b where a.constraint_name = b.constraint_name 
and b.constraint_type = 'P' and a.table_name = 'AA'-------大写 

###查询表的基本信息
-select
utc.column_name,utc.data_type,utc.data_length,utc.data_precision,
utc.data_Scale,utc.nullable,utc.data_default,ucc.comments
from
user_tab_columns utc,user_col_comments ucc
where
utc.table_name = ucc.table_name
and utc.column_name = ucc.column_name
and utc.table_name = 'PRODUCT'
order by
column_id

