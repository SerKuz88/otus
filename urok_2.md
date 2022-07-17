# otus
 поставить PostgreSQL   
 ![image](https://user-images.githubusercontent.com/108919955/179389927-3950a088-2a03-48c7-b91e-21745dab7413.png)   
 
 1. в первой сессии добавить новую запись
 insert into persons(first_name, second_name) values('sergey', 'sergeev');
   сделать select * from persons во второй сессии   
- видите ли вы новую запись и если да то почему?  
- Ответ:
- в первой сессии запись вижу во второй нет, т.к.  read commited не поддерживает грязное чтение
![image](https://user-images.githubusercontent.com/108919955/179390775-a5f06c23-0b1c-4a10-ba67-8807da928fe4.png)   
![image](https://user-images.githubusercontent.com/108919955/179390848-d0c8d773-2e8a-48a0-876b-91e176383732.png)
- завершить первую транзакцию - commit;
- сделать select * from persons во второй сессии
- видите ли вы новую запись и если да то почему?
Ответ:
после коммита во второй сесси появилась запись, т.к. read commited поддерживает фантомное чтение

2. начать новые но уже repeatable read транзакции
- сделать select * from persons во второй сессии
- видите ли вы новую запись и если да то почему?
не вижу, т.к. repeateble read не поддерживает грязное чтение.
