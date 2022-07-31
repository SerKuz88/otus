# otus
создать GCE инстанс типа e2-medium и standard disk 10GB  
установить на него PostgreSQL 13 с дефолтными настройками  
![image](https://user-images.githubusercontent.com/108919955/182013367-08a79c56-ddb2-470a-8dd0-7a13ba5ddea3.png)
  
применить параметры настройки PostgreSQL из прикрепленного к материалам занятия файла  
![image](https://user-images.githubusercontent.com/108919955/182014732-6729ba53-8547-499d-96c0-fbee27b34311.png)
  
выполнить pgbench -i postgres  
![image](https://user-images.githubusercontent.com/108919955/182014853-8ad61794-206b-49d7-bf2a-15d6de1ada58.png)
  
запустить pgbench -c8 -P 60 -T 3600 -U postgres postgres  
дать отработать до конца  
![image](https://user-images.githubusercontent.com/108919955/182017705-55655d26-fe58-42ca-aa7f-fe43b8ac8e8d.png)
  
зафиксировать среднее значение tps в последней ⅙ части работы  
среднее значение из последних 10 значений(573,3  563,3 608,5  632,4 686,1 513,6 603,8 581,5 611,0 624,3 ) = 599,78  

а дальше настроить autovacuum максимально эффективно  
изменены следующие параметры (подчеркнуты красным)  
![image](https://user-images.githubusercontent.com/108919955/182024389-f4b4c632-094f-49d1-8a41-40ba75981610.png)
  
так чтобы получить максимально ровное значение tps на горизонте часа  
попытка номер 2
![image](https://user-images.githubusercontent.com/108919955/182036710-73589687-c59a-4ca4-bfe4-a11a805e8c7f.png)
  
среднее значение из последних 10 значений= 539,47  
попытка номер 3  
см. измененные параметры подчеркнуты  
![image](https://user-images.githubusercontent.com/108919955/182037004-fd3e0721-9b81-4f24-90fd-b9dbe10c8cbc.png)
  
результат:  
![image](https://user-images.githubusercontent.com/108919955/182039195-1039c0c4-2381-49a5-845c-990c7191e945.png)
   
 вывод: максимально равное значение tps на горизонте часа получилось при третьем тесте  
 ![image](https://user-images.githubusercontent.com/108919955/182039337-63320d7a-e19f-4257-9222-505fe0bf7ac5.png)

  
