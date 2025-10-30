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

1. 		N 
	_________
		1
		
2. 		N 
	_________
		2
		
3. 		N 
	_________
		3
		
4. 		N 
	_________
		1
		2
5. 		N 
	_________
		2
		3
		
6. 		N 
	_________
		1
		3

:x: 1\
:x: 2\
:x: 3\
:heavy_check_mark: 4\
:x: 5\
:x: 6