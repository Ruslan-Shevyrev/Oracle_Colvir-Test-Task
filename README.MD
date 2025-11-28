# Oracle_Colvir-Test-Task

Oracle Colvir Test Task.

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

# :six:
Что выведется на экран после выполнения анонимного блока?
```
declare
    a boolean := true;
    b boolean := false;
    c boolean := null;
begin
    if (a and c) then 
        dbms_output.put_line('yes'); 
    else 
        dbms_output.put_line('no'); 
    end if;

    if (b or not c) then 
        dbms_output.put_line('yes'); 
    else 
        dbms_output.put_line('no'); 
    end if;

    if (not (a < c)) then 
        dbms_output.put_line('yes'); 
    else 
        dbms_output.put_line('no'); 
    end if;
end;
```

```
1.  no
	no
	yes
	
2.  yes
	yes
	no
		
3.  no
	no
	no
		
4.  yes
	no
	yes
	
5.  no
	yes
	yes
	
6. 	ORA-06550: line 8, column 14:
	PLS-00306: wrong number or types of arguments in call to '<'
	ORA-06550: line 8, column 3:
	PL/SQL: Statement ignored

```

:x: 1\
:x: 2\
:heavy_check_mark: 3\
:x: 4\
:x: 5\
:x: 6

# :seven:
Значение поля VAL в строке с ID=3
```
with t as
(
    select 1 id, 4 cnt1, 6 cnt2, 7 cnt3 from dual
    union all
    select 2 id, 5 cnt1, 5 cnt2, 8 cnt3 from dual
    union all
    select 3 id, 5 cnt1, 6 cnt2, 9 cnt3 from dual
    union all
    select 4 id, 5 cnt1, 7 cnt2, 9 cnt3 from dual
)
select
    id,
    count(1) over(partition by cnt1) +
    count(1) over(partition by cnt2) as VAL
from t;
```

```
1.  4
	
2.  7
		
3.  5
```

:x: 1\
:x: 2\
:heavy_check_mark: 3

# :eight:
Если изначально таблица пустая. Что будет в Таблице после выполнения анонимного PL/SQL.
```
create table data(ID integer);
BEGIN
    BEGIN
        INSERT INTO DATA VALUES (1);
        SAVEPOINT AD1;
        COMMIT;

        INSERT INTO DATA VALUES (2);
        SAVEPOINT AD2;

        INSERT INTO DATA VALUES (3);
        SAVEPOINT AD3;

        ROLLBACK TO AD2;

        INSERT INTO DATA VALUES (4);
        SAVEPOINT AD4;

        ROLLBACK TO AD1;
    EXCEPTION
        WHEN OTHERS THEN
            NULL;
            ROLLBACK TO AD4;
    END;
    COMMIT;
END;
```

```
1.  1
	2
	4
	
2.  1
	2
	3
		
3.  1
```

:heavy_check_mark: 1\
:x: 2\
:x: 3

# :nine:
Имеется таблица

```
create table DATA(
    ID       number constraint PK_DATA primary key,
    ID_TERR  number not null,
    ID_POK   number not null,
    VALUE    number
);
```
с данными

```
ID	ID_TERR	ID_POK	VALUE
1		10		1	100
2		10		2	120
3		10		2	10
4		20		1	110
5		20		2	200
6		20		2	300
7		20		2	0
```
Какой из запросов позволяет выполнить агрегацию величины VALUE по показателям (ID_POK) в рамках регионов (ID_TERR)

```
1.SELECT
		T.ID_TERR,
		T.ID_POK,
		AGR(T.VALUE) AS SVAL
	FROM DATA T
	GROUP BY T.ID_TERR, T.ID_POK;
	
2. SELECT
		T.ID_TERR,
		T.ID_POK,
		AVG(T.VALUE) OVER (PARTITION BY T.ID_TERR, T.ID_POK)
	FROM DATA T;
		
3. SELECT
		T.ID_TERR,
		T.ID_POK,
		SUM(T.VALUE) AS SVAL
	FROM DATA T
	GROUP BY T.ID_TERR, T.ID_POK;
```

:x: 1\
:x: 2\
:heavy_check_mark: 3

# :one::zero:
Имеется таблица

Что вернёт последний запрос (SELECT) в скрипте:
```
create table parent(
    id number constraint pk_parent primary key
);

insert into parent select rownum from dual connect by rownum <= 10;

create table child(
    id       number constraint pk_child primary key,
    id_parent number constraint fk_child_parent references parent(id) on delete cascade
);

insert into child values(1,2);
insert into child values(2,4);
insert into child values(3,6);
insert into child values(4,8);
insert into child values(5,10);

delete from parent where id = 8;

commit;

select *
from child;
```


```
1. На операторе delete будет ошибка
	delete from parent where id=8
	ORA-02292: integrity constraint (FK_CHILD_PARENT) violated - child record found
	
2. ID   ID_PARENT
	5    10
		
3. ID   ID_PARENT
	1    2
	2    4
	3    6
	5    10
```

:x: 1\
:x: 2\
:heavy_check_mark: 3

# :one::two:
Создана таблица и в неё выполняются вставки (INSERT).
Какой оператор INSERT нарушит уникальность и будет выдана ошибка?

```
ORA-00001: unique constraint

CREATE TABLE T(
    ID_TERR NUMBER NOT NULL,
    ID_KOEF NUMBER NOT NULL,
    ID_YEAR NUMBER NOT NULL,
    NUM_VALUE NUMBER CONSTRAINT UK0 UNIQUE,
    CONSTRAINT UK1 UNIQUE(ID_TERR, ID_KOEF, ID_YEAR),
    CONSTRAINT UK2 UNIQUE(ID_TERR, ID_KOEF)
);

INSERT INTO T VALUES(1,1,1,1);
INSERT INTO T VALUES(1,2,1,2);
INSERT INTO T VALUES(2,1,1,3);
INSERT INTO T VALUES(1,1,1,4);
INSERT INTO T VALUES(1,1,1,5);
INSERT INTO T VALUES(1,1,1,6);
```


```
1. INSERT INTO T VALUES(1,1,1,6)

2. INSERT INTO T VALUES(1,1,1,5)
		
3. INSERT INTO T VALUES(1,1,1,4)
```

:x: 1\
:x: 2\
:heavy_check_mark: 3

# :one::three:
Выберите правильный результат выполнения запроса select:

```
create table table_1(n number);
create table table_2(n number);

insert into table_1 values(1);
insert into table_1 values(2);

insert into table_2 values(1);
insert into table_2 values(3);

select n
from table_1
union all
select n
from table_2
order by n;
```


```
1.  N
	1
	2
	3
		
2.  N
	1
	
3.  N
	1
	1
	2
	3
```

:x: 1\
:x: 2\
:heavy_check_mark: 3


# :one::four:
План выполнения запросов.

Создана таблица и наполнена данными следующим скриптом:

```
CREATE TABLE DATA(
  ID  NUMBER CONSTRAINT PK_DATA PRIMARY KEY,
  VAL NUMBER NOT NULL
);

INSERT INTO DATA
SELECT
  ROWNUM,
  1 AS VAL
FROM
  DUAL
CONNECT BY ROWNUM <= 1000000;

COMMIT;

BEGIN
  DBMS_STATS.gather_table_stats(user, tabname => 'DATA', cascade => true);
END;
/
```
Далее выполняется ряд запросов, необходимо выбрать наиболее вероятные
пути доступа к данным. Пути доступа в вариантах ответов приведены в той же
последовательности, что и запросы SELECT.
```
SELECT SUM(1)
   FROM DATA

SELECT *
   FROM DATA D
   WHERE D.ID = 1234

SELECT COUNT(*)
   FROM DATA D
   WHERE D.ID BETWEEN 10 AND 200

SELECT SUM(VAL)
   FROM DATA D
   WHERE D.ID > 10
```

```
1.  TABLE ACCESS FULL
	INDEX RANGE SCAN
	TABLE ACCESS FULL
	INDEX UNIQUE SCAN
	INDEX FAST FULL SCAN
		
2.  INDEX FAST FULL SCAN
	INDEX UNIQUE SCAN
	TABLE ACCESS FULL
	INDEX RANGE SCAN
	TABLE ACCESS FULL
	
3.  TABLE ACCESS FULL
	INDEX FAST FULL SCAN
	INDEX RANGE SCAN
	TABLE ACCESS FULL
	INDEX UNIQUE SCAN
```

:x: 1\
:x: 2\
:heavy_check_mark: 3

# :one::five:
Выберите наиболее верную группу высказываний.

1. Представления (VIEW) главным образом используются для ускорения выполнения запросов. Они связаны с кэшированием результатов одного запроса. Индексы в БД используются в 90% случаев, чтобы обеспечить выполнение уникальности для первичных и уникальных ключей.
Выполнение SQL запросов из PL/SQL кода приводит к переключению контекста (SQL ↔ PL/SQL), что является очень ресурсоёмкой операцией.

2. Обычные таблицы в БД организованы в виде «кучи». Негативная сторона наличия индексов – это замедление вставок и обновлений записей в таблицах. Пользователь и схема – это эквивалентные понятия в БД Oracle. Ограничения типа foreign key не стоит использовать там, где и так очевидно наличие логической связи между таблицами. Переменные связанные (bind variables) стоит использовать вообще во всех SQL операторах, это эффективно во всех случаях.

3. Частое применение представлений (VIEW) в базе данных используется для упрощения написания сложных SQL запросов. Само представление не содержит в себе данных. Индексы наиболее часто эффективны при извлечении небольшого количества записей из таблиц (s). Иногда выбор всех записей из таблицы при помощи индекса может быть эффективнее, чем полное сканирование таблицы (TABLE FULL SCAN). Оптимизатор SQL запросов в БД — это математическая модель, которая принимает на свой вклад статистику по объектам в БД, сам запрос SQL и генерирует несколько планов выполнения, далее из этих планов выбирается оптимальный.

:x: 1\
:x: 2\
:heavy_check_mark: 3

<table>
	<tr>
		<td valign="center" width="49%"><img src="https://github.com/Ruslan-Shevyrev/Ruslan-Shevyrev/blob/main/logoRS/logo_mini.gif" title="logo"></td>
		<td valign="center" width="49%"><img src="https://github.com/Ruslan-Shevyrev/Ruslan-Shevyrev/blob/main/logoRS/logoRS_FULL.png" title="RuslanShevyrev"></td>
	</tr>
</table>