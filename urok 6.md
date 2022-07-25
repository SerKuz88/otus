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
