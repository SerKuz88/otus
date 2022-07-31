# otus
создать GCE инстанс типа e2-medium и standard disk 10GB  
установить на него PostgreSQL 13 с дефолтными настройками  
![image](https://user-images.githubusercontent.com/108919955/182013367-08a79c56-ddb2-470a-8dd0-7a13ba5ddea3.png)
  
применить параметры настройки PostgreSQL из прикрепленного к материалам занятия файла  
выполнить pgbench -i postgres  
запустить pgbench -c8 -P 60 -T 3600 -U postgres postgres  
дать отработать до конца  
зафиксировать среднее значение tps в последней ⅙ части работы  
а дальше настроить autovacuum максимально эффективно  
так чтобы получить максимально ровное значение tps на горизонте часа  
