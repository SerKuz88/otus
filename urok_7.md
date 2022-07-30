# otus
1 создайте новый кластер PostgresSQL 13 (на выбор - GCE, CloudSQL)  
2 зайдите в созданный кластер под пользователем postgres  
![image](https://user-images.githubusercontent.com/108919955/181925586-6fe7dc01-df1a-4723-a4bd-05c27c01b52b.png)
  
3 создайте новую базу данных testdb  
4 зайдите в созданную базу данных под пользователем postgres  
![image](https://user-images.githubusercontent.com/108919955/181925694-f31b518f-eadf-409f-82f3-a0e8b648f891.png)
  
5 создайте новую схему testnm  
6 создайте новую таблицу t1 с одной колонкой c1 типа integer  
7 вставьте строку со значением c1=1  
![image](https://user-images.githubusercontent.com/108919955/181925788-7f3b5668-91d8-4115-bcb1-0182ef709cfe.png)
  
8 создайте новую роль readonly  
9 дайте новой роли право на подключение к базе данных testdb  
10 дайте новой роли право на использование схемы testnm  
11 дайте новой роли право на select для всех таблиц схемы testnm  
![image](https://user-images.githubusercontent.com/108919955/181926231-ea5868d9-7822-46cb-827b-a6d18335d186.png)
  
12 создайте пользователя testread с паролем test123  
13 дайте роль readonly пользователю testread  
![image](https://user-images.githubusercontent.com/108919955/181926314-15142a6b-fe8c-4603-bd81-858ce0117aba.png)
  
14 зайдите под пользователем testread в базу данных testdb  
![image](https://user-images.githubusercontent.com/108919955/181933347-7ed53661-c735-4923-8e89-676a57917797.png)
  
15 сделайте select * from t1;  
16 получилось? (могло если вы делали сами не по шпаргалке и не упустили один существенный момент про который позже)  
17 напишите что именно произошло в тексте домашнего задания  
18 у вас есть идеи почему? ведь права то дали?  
![image](https://user-images.githubusercontent.com/108919955/181933473-49c586c9-cee1-4c9f-bf72-c2d5f2761b1e.png)
  
  не получилось, т.к. если не указывать схему, то таблица создается по search_path  
  ![image](https://user-images.githubusercontent.com/108919955/181933567-174af75a-fe84-4dbe-875d-0a3c5537e033.png)
  
19 посмотрите на список таблиц  
20 подсказка в шпаргалке под пунктом 20  
21 а почему так получилось с таблицей (если делали сами и без шпаргалки то может у вас все нормально)  
22 вернитесь в базу данных testdb под пользователем postgres  
23 удалите таблицу t1  
24 создайте ее заново но уже с явным указанием имени схемы testnm  
25 вставьте строку со значением c1=1  
26 зайдите под пользователем testread в базу данных testdb  
27 сделайте select * from testnm.t1;  
28 получилось?  
29 есть идеи почему? если нет - смотрите шпаргалку  
30 как сделать так чтобы такое больше не повторялось? если нет идей - смотрите шпаргалку  
31 сделайте select * from testnm.t1;  
32 получилось?  
33 есть идеи почему? если нет - смотрите шпаргалку  
31 сделайте select * from testnm.t1;  
32 получилось?  
33 ура!  
34 теперь попробуйте выполнить команду create table t2(c1 integer); insert into t2 values (2);  
35 а как так? нам же никто прав на создание таблиц и insert в них под ролью readonly?  
36 есть идеи как убрать эти права? если нет - смотрите шпаргалку  
37 если вы справились сами то расскажите что сделали и почему, если смотрели шпаргалку - объясните что сделали и почему выполнив указанные в ней команды  
38 теперь попробуйте выполнить команду create table t3(c1 integer); insert into t2 values (2);  
39 расскажите что получилось и почему   