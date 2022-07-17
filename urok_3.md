# otus
• сделать в GCE инстанс с Ubuntu 20.04 или развернуть докер любым удобным способом
• поставить на нем Docker Engine   
![image](https://user-images.githubusercontent.com/108919955/179409831-a0f665c1-de24-44b1-b216-d67c14c42ba6.png)
   
   сделать каталог /var/lib/postgres
• развернуть контейнер с PostgreSQL 14 смонтировав в него /var/lib/postgres   
![image](https://user-images.githubusercontent.com/108919955/179410747-db2fd2b4-21b8-42a3-9a42-16ff7ac8a82a.png)   
   
 развернуть контейнер с клиентом postgres   
 • подключится из контейнера с клиентом к контейнеру с сервером и сделать
таблицу с парой строк   
![image](https://user-images.githubusercontent.com/108919955/179410845-40fd23cd-8583-4d5d-ba0c-111ebffe303b.png)
![image](https://user-images.githubusercontent.com/108919955/179411067-5a0109b5-8013-4859-bc73-fdb95049f2c5.png)
   
подключится к контейнеру с сервером с ноутбука/компьютера извне инстансов GCP/места установки докера   
сервер на котором установлен докер - 158.160.1.246   
сторонний сервер - "server-iz-vne"   
пингуем, удаленно подключаемся к постгресу на 158.160.1.246, проверяем наличие созданной таблицы   
![image](https://user-images.githubusercontent.com/108919955/179413951-0404d4a7-1651-456e-a04b-53fe3ed25fcb.png)   
   
удалить контейнер с сервером   
![image](https://user-images.githubusercontent.com/108919955/179416677-4ed9fa70-3e88-440c-b88b-f00e68fa7d37.png)
   
• создать его заново   
• подключится снова из контейнера с клиентом к контейнеру с сервером   
• проверить, что данные остались на месте   
![image](https://user-images.githubusercontent.com/108919955/179416898-e0f5e290-7433-436f-9a11-9a1157aada1c.png)
