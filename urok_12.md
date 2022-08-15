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
  
3 тестирование, добавляем следующие параметры:  
ALTER SYSTEM SET  maintenance_work_mem = '128MB';  
ALTER SYSTEM SET  checkpoint_completion_target = '0.9';  
ALTER SYSTEM SET  wal_buffers = '16MB';  
ALTER SYSTEM SET  default_statistics_target = '100';  
ALTER SYSTEM SET  random_page_cost = '1.1';  
![image](https://user-images.githubusercontent.com/108919955/184646867-cf84693d-34e6-409a-892f-c8d046464a29.png)  
данные параметры не принесли прироста tps, даже в каких то моментах он снизился.  

4 тестирование:  
ALTER SYSTEM SET  effective_io_concurrency = '200';  
ALTER SYSTEM SET  work_mem = '2621kB';  
![image](https://user-images.githubusercontent.com/108919955/184647734-abb946cf-cabc-4797-a91a-6698d8deafe9.png)  
результат схож с 3 тестированием  
  
5 тестирование:  
ALTER SYSTEM SET max_worker_processes = '2';  
ALTER SYSTEM SET max_parallel_workers_per_gather = '1';  
ALTER SYSTEM SET max_parallel_workers = '2';  
ALTER SYSTEM SET max_parallel_maintenance_workers = '1';  
![image](https://user-images.githubusercontent.com/108919955/184648705-8249f1c1-172c-4e01-9aae-20a140b697db.png)  
с этими параметрами показатель tps немного увеличился, но не сильно.  

6 тестирование:  
ALTER SYSTEM SET synchronous_commit = off;  ![image](https://user-images.githubusercontent.com/108919955/184649786-924cd857-4611-4581-8d6a-b37dfebc2d8a.png)  
включение асинхронного режима дало нам прирост tps процентов на 30-40.  

