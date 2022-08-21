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
    
3 ВМ использовать как реплику для чтения и бэкапов  
(подписаться на таблицы из ВМ №1 и №2 ).   
Небольшое описание, того, что получилось.  
* реализовать горячее реплицирование для высокой доступности на   
4ВМ. Источником должна выступать ВМ №3. Написать с какими   
проблемами столкнулись.   

