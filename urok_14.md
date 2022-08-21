# otus
На 1 ВМ создаем таблицы test для записи, test2 для запросов на   
чтение.   
![image](https://user-images.githubusercontent.com/108919955/185779128-2603b9c7-b761-4bde-9a81-148d5992cf3b.png)   
   
Создаем публикацию таблицы test    
![image](https://user-images.githubusercontent.com/108919955/185780110-97cb855b-8774-4923-865a-5047dd433a36.png)   
и подписываемся на публикацию таблицы test2 с ВМ №2.   
![image](https://user-images.githubusercontent.com/108919955/185781576-cc6476fd-b5a6-4705-a5cd-d40c3a8e2bf0.png)   
![image](https://user-images.githubusercontent.com/108919955/185781612-1261402d-1b6d-42b1-a804-b5e185edde07.png)    
   
На 2 ВМ создаем таблицы test2 для записи, test для запросов на   
чтение.   
![image](https://user-images.githubusercontent.com/108919955/185780063-5b509289-60e5-4883-9454-4f970814fb48.png)   
    
Создаем публикацию таблицы test2 и подписываемся на публикацию таблицы test1 с ВМ №1.   
![image](https://user-images.githubusercontent.com/108919955/185781716-8b1443fd-5e97-463f-b6cb-fdf577dba623.png)   
![image](https://user-images.githubusercontent.com/108919955/185781842-b5e6bc1e-7156-413e-ac47-ae53d4f3de31.png)   
    
3 ВМ использовать как реплику для чтения и бэкапов  (подписаться на таблицы из ВМ №1 и №2 ).    
Небольшое описание, того, что получилось.   
Создал две таблицы на 3 виртуальной машине:    
![image](https://user-images.githubusercontent.com/108919955/185782193-87442bb0-c4e8-4666-a6f7-3aac99648fb0.png)     
Добавил публикацию на перевой виртуальной машине по таблице test2  
![image](https://user-images.githubusercontent.com/108919955/185782328-0a6bcbb5-b36a-45a0-8382-cf6519e96018.png)   
Добавил публикацию на второй виртуальной машине по таблице test1   
![image](https://user-images.githubusercontent.com/108919955/185782721-49f722c5-95df-4b0b-b791-fdba81831782.png)   
   
Создаем подписку на 3 вирт машине для всех таблиц 1 виртуальной машины:   
![image](https://user-images.githubusercontent.com/108919955/185782488-8a2bd875-5b11-49a9-87ba-e52bc4843389.png)   
![image](https://user-images.githubusercontent.com/108919955/185782551-3840d7cb-d071-4720-8739-44d3c76af9d7.png)   
   
Создаем подписку на 3 вирт машине для всех таблиц 2 виртуальной машины:   
![image](https://user-images.githubusercontent.com/108919955/185782859-9c2c4742-a6ec-4388-b33c-dd3f0e2fba0b.png)   
![image](https://user-images.githubusercontent.com/108919955/185783115-6e495dd8-5947-4055-9bbd-ceaec091cb7d.png)   

В итоге получаем, например, если добавить строку (111, test1) на первую вирт машину, она следом реплицируется на вторую вирт машину и уже из первой и второй эти строки реплицируются на 3 вирт машине:   
![image](https://user-images.githubusercontent.com/108919955/185783540-f457eaa8-9af0-4b81-a058-348be9cec832.png)   
    
    

* реализовать горячее реплицирование для высокой доступности на   
4ВМ. Источником должна выступать ВМ №3. Написать с какими   
проблемами столкнулись.   

1. настраиваем IP адрес на ВМ3 (прописываем IP ВМ3)   
![image](https://user-images.githubusercontent.com/108919955/185798309-21218c5a-3904-4a67-ad92-5e98946509bf.png)   
2. создаем специальные праава на репликацию   
CREATE ROLE test WITH REPLICATION PASSWORD 'testpassword' LOGIN;   
3.редактируем pg_hba.conf (прописываем IP ВМ4)  
![image](https://user-images.githubusercontent.com/108919955/185798413-8dacf34e-01b1-401d-a4d6-49c0d7404cb0.png)   
4. перезагружаем ВМ3   
5. на ВМ4 удаляем каталог main и на месте его создаем пустой такойже  
sudo -u postgres rm -r /var/lib/postgresql/13/main  
sudo -u postgres mkdir /var/lib/postgresql/13/main  
sudo -u postgres chmod 700 /var/lib/postgresql/13/main  
6.копируем из ВМ3 в ВМ4 каталог main:    
sudo -u postgres pg_basebackup -h 10.129.0.19 -p 5432 -U test -D /var/lib/postgresql/13/main/ -Fp -Xs -R    
7. перезагружаемся   
8. на ВМ3 стал виден ip базы репликации ВМ4:   
![image](https://user-images.githubusercontent.com/108919955/185798650-2182d326-61ae-49de-afde-119ce7c73979.png)   
  




