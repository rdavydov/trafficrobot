User (clien) API
================

Юзер должен иметь возможность создать себе АПИ ключ, и по 
ключу запрашивать контент на коннекторах.


* Команда боту `/getapikey`. Возвращаем или геренируем юзеру апи ключ

    Storage:
    
        {userid}_apikey = {apikey} ; для данного юзера сохраняем апи ключ
        {apikey}_userid = {userid} ; reverse lookup по апи ключу
        

User API
---------

REST ендпоинт:

* `/api/{apikey}/get_last/{connectorkey}`. Возвращает последние переданные на коннектор данные. 
Данные самоуничтожаются через 24h. Для этого модели Коннектора прийдется
сохранять для каждых переданных данных такую структуру:

    Storage:
    
        {connectorkey}_last = {data}
        
    Т.о. алгоритм действия для такого запроса:

    * Убедиться что для текущего юзера это валидный ключ
    * Убедиться что данный коннектор таки принадлежит этому юзеру
    * Запросить и отдать последние данные по этому ключу