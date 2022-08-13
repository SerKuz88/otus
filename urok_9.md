# otus
1.Настройте сервер так, чтобы в журнал сообщений сбрасывалась информация о блокировках, удерживаемых более 200 миллисекунд. Воспроизведите ситуацию, при которой в журнале появятся такие сообщения.   
до настроек:  
![image](https://user-images.githubusercontent.com/108919955/184071002-6c11dfa3-08b2-4f73-83c6-e76e182ed10d.png)  
  
после настроек:  
![image](https://user-images.githubusercontent.com/108919955/184072158-c42685b0-b216-462b-a72c-946fc2008f27.png)  
  
 пример:  
 первая сессия  
 ![image](https://user-images.githubusercontent.com/108919955/184470550-46e327a1-bfb2-430d-86d8-d2268c8818c7.png)  
 вторая сессия  
 ![image](https://user-images.githubusercontent.com/108919955/184470610-2fa87ff6-9834-4a30-8e72-eedeee5a42d2.png)  

запрос показывает следующие блокировки:  
![image](https://user-images.githubusercontent.com/108919955/184470723-320e7498-6594-48da-b54a-e535e8da0eca.png)
  
в логе появились записи об этой блокировке:  
![image](https://user-images.githubusercontent.com/108919955/184470770-59dc5c00-d780-4907-a8ad-1e8116798819.png)  
  
2.Смоделируйте ситуацию обновления одной и той же строки тремя командами UPDATE в разных сеансах. Изучите возникшие блокировки в представлении pg_locks и убедитесь, что все они понятны. Пришлите список блокировок и объясните, что значит каждая.   
  
Добавляем еще одну транзкцию к текущим двум:  
![image](https://user-images.githubusercontent.com/108919955/184472926-f35c47b4-5af3-4c71-bd3a-b1894689e443.png)  
Список блокировок:  
![image](https://user-images.githubusercontent.com/108919955/184472883-b109b18e-3e84-40fc-91a2-5bd6bca932a3.png)  
  
здесь мы видим, что:  
Три транзакции с типом relation в режиме RowExclusiveLock устанавились для изменения строк;  
две из них ожидают блокировку типа tuple для обновляемой строки.


3.Воспроизведите взаимоблокировку трех транзакций. Можно ли разобраться в ситуации постфактум, изучая журнал сообщений?  
1 сессия изменяет строку 1:  
![image](https://user-images.githubusercontent.com/108919955/184475251-19cbc4e9-31c4-48cf-aaee-1a87d8563b6f.png)
2 сессия изменяет строку 2:  
![image](https://user-images.githubusercontent.com/108919955/184475274-2a760154-8295-46a7-a5e5-5a23ebadd9f8.png)  
3 сессия изменяет строку 3:  
![image](https://user-images.githubusercontent.com/108919955/184475290-4c903033-43e1-4d42-bd78-0bc68c3a02e7.png)  
  
потом:
первая сессия изменят строку 2  
![image](https://user-images.githubusercontent.com/108919955/184475362-dd934b60-1c76-4f1b-8ac2-da1bd0fb8aa6.png)  
вторая сессия изменяет строку 3  
![image](https://user-images.githubusercontent.com/108919955/184475389-edcfc2c2-d8dc-4923-8dcd-f9a8eff028c8.png)  
и  
третья сессия в этот момент решает изменить строку 1  
![image](https://user-images.githubusercontent.com/108919955/184475425-7791ca74-fecf-4d9d-a113-dfde1b51df82.png)  
  
получаем ошибку: deadlock detected    

4.Могут ли две транзакции, выполняющие единственную команду UPDATE одной и той же таблицы (без where), заблокировать друг друга?  
5.Попробуйте воспроизвести такую ситуацию.  


