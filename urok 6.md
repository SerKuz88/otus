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
делаем файловую систему, смотрим uuid   
![image](https://user-images.githubusercontent.com/108919955/180824439-1ddc001c-2840-4409-a82f-497903170cf7.png)   
![image](https://user-images.githubusercontent.com/108919955/180824984-e56437bb-4d07-4933-a13a-958a623b6ab2.png)
   
создаем директорию   
![image](https://user-images.githubusercontent.com/108919955/180826102-dccce3f9-8d8a-4adc-bd43-710341136039.png)
   
добавил uuid в fstab   
![image](https://user-images.githubusercontent.com/108919955/180828434-3bd6d800-ab97-4b36-802f-94fb845191d5.png)   
   
перенесите содержимое /var/lib/postgres/14 в /mnt/data - mv /var/lib/postgresql/14 /mnt/data   
![image](https://user-images.githubusercontent.com/108919955/180829397-8c4b5bde-3324-4942-a75b-60cabbfb2450.png)   
   
попытайтесь запустить кластер - sudo -u postgres pg_ctlcluster 14 main start   
ответ: не запустится, т.к. в файле postgresql.conf параметр data_directory имеет старый котолог, который уже не существует   
![image](https://user-images.githubusercontent.com/108919955/180830856-56c993ba-b0fe-485f-8c1b-d801ae76fb17.png)


