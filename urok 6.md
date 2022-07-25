# otus
создайте виртуальную машину c Ubuntu 20.04    
поставьте на нее PostgreSQL 14 через sudo apt   
   
![image](https://user-images.githubusercontent.com/108919955/180815689-f507c34a-4ec6-4ba5-9cef-77db0b1b314c.png)

проверьте что кластер запущен через sudo -u postgres pg_lsclusters   
![image](https://user-images.githubusercontent.com/108919955/180816060-873e3eec-95d5-463a-9c83-806ac5240bfd.png)
   
зайдите из под пользователя postgres в psql и сделайте произвольную таблицу с произвольным содержимым postgres=# create table test(c1 text); postgres=# insert into test values('1'); \q   

![image](https://user-images.githubusercontent.com/108919955/180816773-5ff0cecc-0057-4356-9567-fd69bf207e17.png)
   
остановите postgres например через sudo -u postgres pg_ctlcluster 14 main stop   
![image](https://user-images.githubusercontent.com/108919955/180817710-6bb6c8b6-a158-4112-b163-0112f732fd05.png)
   
создайте новый standard persistent диск   
Имеем диск vdb на 12 гб   
![image](https://user-images.githubusercontent.com/108919955/180818947-cc1e79f2-19db-4992-955e-f484f488f787.png)   
разбиваем диск через fdisk  
![image](https://user-images.githubusercontent.com/108919955/180821724-85c5dd05-be26-4865-a2c2-a77d73f9841d.png)   
![image](https://user-images.githubusercontent.com/108919955/180821788-04c5aabf-86df-4847-88db-37687b295d74.png)   
делаем файловую систему, смотрим uuid, перезагружаем сервер   
![image](https://user-images.githubusercontent.com/108919955/180823106-2f3ad721-85c5-41a4-aadd-1d65567824b2.png)
