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
![image](https://user-images.githubusercontent.com/108919955/181933624-82366bc9-416f-41d8-8a39-190bedd48643.png)
  
22 вернитесь в базу данных testdb под пользователем postgres  
23 удалите таблицу t1  
24 создайте ее заново но уже с явным указанием имени схемы testnm  
25 вставьте строку со значением c1=1  
![image](https://user-images.githubusercontent.com/108919955/181933720-903d82e2-1b2c-428c-bf4f-7de221ac56a3.png)
  
26 зайдите под пользователем testread в базу данных testdb  
27 сделайте select * from testnm.t1;  
28 получилось?  
29 есть идеи почему? если нет - смотрите шпаргалку  
![image](https://user-images.githubusercontent.com/108919955/181933828-eade6095-4976-443b-a3f9-188061540d28.png)
  
  Не получилось, т.к. талицу пересоздали, грант слетел.  
  
30 как сделать так чтобы такое больше не повторялось? если нет идей - смотрите шпаргалку  
![image](https://user-images.githubusercontent.com/108919955/181933932-0d024b54-d84b-42ab-8693-e4c99b4c9879.png)
  
  заново выдал грант на просмотр всех таблиц  
31 сделайте select * from testnm.t1;  
32 получилось?  
33 есть идеи почему? если нет - смотрите шпаргалку  
31 сделайте select * from testnm.t1;  
32 получилось?  
33 ура!  
![image](https://user-images.githubusercontent.com/108919955/181933977-8e07e697-c6fe-4727-a395-f3a433d4ca3e.png)
  
34 теперь попробуйте выполнить команду create table t2(c1 integer); insert into t2 values (2);  
![image](https://user-images.githubusercontent.com/108919955/181934151-cb559aac-ad3c-40fa-a66b-fe8d836000be.png)
  
35 а как так? нам же никто прав на создание таблиц и insert в них под ролью readonly?  
таблица создалась, т.к. опять не написана схема, по умолчанию создается в public  
  
36 есть идеи как убрать эти права? если нет - смотрите шпаргалку  
37 если вы справились сами то расскажите что сделали и почему, если смотрели шпаргалку - объясните что сделали и почему выполнив указанные в ней команды  
![image](https://user-images.githubusercontent.com/108919955/181934510-6b43f762-c8e4-4a3f-8654-8ce047af8364.png)
  
  отменили привилегии для роли public.  
    
38 теперь попробуйте выполнить команду create table t3(c1 integer); insert into t2 values (2);  
![image](https://user-images.githubusercontent.com/108919955/181934589-2ed7e3d8-4f64-441c-9295-cf0271aa71f4.png)
  
39 расскажите что получилось и почему   
мы отменили только возможность создавать новые таблицы в схеме public, поэтому таблица t3 не создалась, но обращаться по умолчанию к схеме public и вставлять туда данные мы не отменяли, поэтому в таблицу t2 мы смогли вставить запись  
