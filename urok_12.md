# otus
• развернуть виртуальную машину любым удобным способом  
• поставить на неё PostgreSQL 14 любым способом  
![image](https://user-images.githubusercontent.com/108919955/184637999-2e289c9a-3114-4b73-ab2d-8a25e28b175b.png)  
  
• настроить кластер PostgreSQL 14 на максимальную производительность не обращая внимание на возможные проблемы с надежностью в случае аварийной перезагрузки виртуальной машины  
• нагрузить кластер 
• написать какого значения tps удалось достичь, показать какие параметры в  
какие значения устанавливали и почему   
   
      
1 тестирование без настроек, все по умолчанию:   
![image](https://user-images.githubusercontent.com/108919955/184644009-4d9831ba-bedd-40d7-b1b5-0fadd63adc45.png)  
средний tps = 200  
  
2 тестирование:  
ALTER SYSTEM SET  shared_buffers = '512MB';  
ALTER SYSTEM SET  effective_cache_size = '1536MB';  
![image](https://user-images.githubusercontent.com/108919955/184645598-ad2a81a3-b1b4-47e7-9e5a-1339d958fa4c.png)  
видимый прирост в tps - примерно 10%  

