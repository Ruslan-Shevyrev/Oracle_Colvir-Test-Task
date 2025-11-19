# :one:
Выберите правильный результат выполнения запроса select
```
create table table_1(n number);
create table table_2(n number);
create table table_3(n number);

insert into table_1 values(1);
insert into table_1 values(2);

insert into table_2 values(1);
insert into table_2 values(3);

insert into table_3 values(2);
insert into table_3 values(3);

select * from table_1
where n not in (select n from table_2 where n in(select * from table_3));
```
```
1. 		N 
		1
		
2. 		N 
		2
		
3. 		N 
		3
		
4. 		N 
		1
		2
		
5. 		N 
		2
		3
		
6. 		N 
		1
		3
```

:x: 1\
:x: 2\
:x: 3\
:heavy_check_mark: 4\
:x: 5\
:x: 6

# :two:
Приведен запрос. Выбрать один верный аналог (заменитель).
```
SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USERS_SYSTEMS TUS
    LEFT JOIN T_USERS TU
        ON TUS.USER_ID = TU.USER_ID
```

```
1. SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USERS_SYSTEMS TUS,
    T_USERS TU
WHERE
    TU.USER_ID = TUS.USER_ID
		
2. SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USERS_SYSTEMS TUS,
    T_USERS TU
WHERE
    TU.USER_ID = TUS.USER_ID(+)
		
3. SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USERS TU
FULL JOIN
    T_USERS_SYSTEMS TUS
        ON TUS.USER_ID = TU.USER_ID
		
4. SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USER_SYSTEMS TUS,
    T_USERS TU
WHERE
    TUS.USER_ID = TU.USER_ID(+)
		
5. SELECT
    TUS.SYSTEM_ID,
    TU.USER_LOGIN
FROM
    T_USERS_SYSTEMS TUS,
    T_USERS TU
WHERE
    TU.USER_ID(+) = TUS.USER_ID
```

:x: 1\
:x: 2\
:x: 3\
:x: 4\
:heavy_check_mark: 5

# :three:
Приведен запрос. Каким из запросов его можно заменить?
```
SELECT
    TU.USER_LOGIN
FROM
    T_USERS TU
WHERE
    TU.USER_ID IN (SELECT TUS.USER_ID
                   FROM T_USERS_SYSTEMS TUS)
```

```
1. SELECT
    TU.USER_LOGIN
FROM
    T_USERS TU,
    T_USERS_SYSTEMS TUS
WHERE
    TUS.USER_ID = TU.USER_ID
    AND TUS.USER_ID = TUS.USER_ID
		
2. SELECT
    TU.USER_LOGIN
FROM
    T_USERS TU
WHERE
    EXISTS (
        (SELECT 1
         FROM T_USERS_SYSTEMS TUS
         WHERE TUS.USER_ID = TU.USER_ID)
    )
    AND 1=1
		
3. SELECT
    TU.USER_LOGIN
FROM
    T_USERS TU
LEFT JOIN
    T_USERS_SYSTEMS TUS
ON (TUS.USER_ID = TU.USER_ID AND 0<1)
		
4. SELECT
    TU.USER_LOGIN
FROM
    T_USERS TU,
    T_USERS_SYSTEMS TUS
WHERE
    TU.USER_ID(+) = TUS.USER_ID
```

:x: 1\
:heavy_check_mark: 2\
:x: 3\
:x: 4

# :four:
Выберите правильный результат выполнения команд.
```
create global temporary table buff_study
(id        number,
 id_pok    number,
 value     number)
on commit delete rows /*+ first_row */;

insert into buff_study(id,id_pok,value) values(1,220,3456);
insert into buff_study(id,id_pok,value) values(2,440,3456);
insert into buff_study(id,id_pok,value) values(3,20,3456);

select *
from
    buff_study;

commit;

select *
from
    buff_study;
```

```
1. ORA-00901: invalid CREATE command
	ORA-00942 Table or view does not exist
	ORA-00942 Table or view does not exist
	ORA-00942 Table or view does not exist
	ORA-00942 Table or view does not exist
	
	commit comlete
	
	ORA-00942 Table or view does not exist	
	
2. 	ID		ID_POK		VALUE 
	1		220			3456
	2		440			3456
	3		20			3456
		
	commit comlete
	
	ID		ID_POK		VALUE 
		
3.  ID		ID_POK		VALUE 
	1		220			3456
	2		440			3456
	3		20			3456
		
	commit comlete
	
	ID		ID_POK		VALUE 
	1		220			3456
	2		440			3456
	3		20			3456
		
4. ID		ID_POK		VALUE 
	2		440			3456
	3		20			3456
		
	commit comlete
	
	ID		ID_POK		VALUE 
	
5.  ID		ID_POK		VALUE 
	1		220			3456
	2		440			3456
	3		20			3456
		
	commit comlete
	
	ID		ID_POK		VALUE 
	2		440			3456
	3		20			3456

```

:x: 1\
:heavy_check_mark: 2\
:x: 3\
:x: 4\
:x: 5

# :five:
Какой запрос гарантированно вернет максимальное значение VAL.

```
1. with t as
	(
		select 2 val from dual
		union all
		select 3 val from dual
		union all
		select 1 val from dual
	)
	select
		val
	from
	(
		select val from t order by val desc
	)
	where
		rownum = 1
	
2. 	with t as
	(
		select 2 val from dual
		union all
		select 3 val from dual
		union all
		select 1 val from dual
	)
	select
		val
	from
	(
		select val from t order by val asc
	)
	where
		rownum = 1
		
3.  with t as
	(
		select 2 val from dual
		union all
		select 3 val from dual
		union all
		select 1 val from dual
	)
	select val from t where rownum = 1 order by val desc
		
4. with t as
	(
		select 2 val from dual
		union all
		select 3 val from dual
		union all
		select 1 val from dual
	)
	select val from t where rownum = max(val)

5.  with t as
	(
		select 2 val from dual
		union all
		select 3 val from dual
		union all
		select 1 val from dual
	)
	select max(val) from t where rownum = 1

```

:heavy_check_mark: 1\
:x: 2\
:x: 3\
:x: 4\
:x: 5