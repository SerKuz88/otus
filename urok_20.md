# otus
Секционировать большую таблицу из демо базы flights   
   
1. Необходимо провести анализ таблицы для определения ключа по которому можно разбить таблицу.    
Определил возможные поля: flight_no, departure_airport, aircraft_code, scheduled_departure   
   
   ![image](https://user-images.githubusercontent.com/108919955/192154418-418ac13e-7398-4efd-905b-a41f5ba045d8.png)   
flight_no имеет 710 уникальных номеров   
   
   ![image](https://user-images.githubusercontent.com/108919955/192154514-9b8f38a5-4cc3-4f9b-af0f-ca8eaeae3d85.png)   
departure_airport имеет 104 уникальных аэропорта для отправления   
    
    ![image](https://user-images.githubusercontent.com/108919955/192154627-0dfa15d5-5e06-4f5f-84f8-85298b57ad68.png)   
aircraft_code имеет 8 уникальных кодов самолетов   
   
   ![image](https://user-images.githubusercontent.com/108919955/192154732-c60fc7d6-521d-40ad-a6cb-da3c30b8d9a4.png)   
scheduled_departure имеет разбиение на три месяца.   
   
Остановлюсь на последнем варианте, сделаю три основных партиции, по месяцам: июль, август, сентябрь.   
   
2. создаю таблицу, секционированную по полю scheduled_departure   
   
   ![image](https://user-images.githubusercontent.com/108919955/192155429-ed9b2050-b081-4cb9-8bb6-1b1212afa194.png)

