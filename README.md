# currency_exchange_dynamics

Задача с сайта hh.ru

Скрейпинг исторической динамики валютного курса заданной валюты (венгерский форинт, гонконгский доллар и т.п.) с сайта ЦБР в любую реляционную базу данных (за весь период наблюдений). Дано: URL https://cbr.ru/currency_base/dynamics/, название валюты в том виде, в котором она записана на сайте, например: “фунт стерлингов Соединен”. Ожидаемый результат программы на Python 3: таблица или несколько таблиц в любой реляционной базе данных с ежедневным курсом заданной валюты. Внимание: запрос к API ЦБР не засчитывается как решенное тестовое задание. Ожидаемый результат выполнения задания: zip-архив git-репозитория с полной историей разработки, и как минимум: с файлом README.md в корневой директории с инструкциями по запуску проекта, файлом requirements.txt для создания виртуального окружения, файлом run.py для осуществления скрейпинга.

Решение: Для получения данных будем проходить 2 этапа:
  1) Формировать get-запросы библиотеки request;
  2) Парсить результаты запросов библиотекой beautifulsoup4. 
  
Сначала получим список названий всех валют с их кодами (VAL_NM_RQ) со стартовой страницы, для этого будем использовать get-запрос "https://cbr.ru/currency_base/dynamics/". Для получения данных по конкретной валюте будем используется get-запрос вида "https://cbr.ru/currency_base/dynamics/?UniDbQuery.Posted={Posted}&UniDbQuery.so={so}&UniDbQuery.mode={mode}&UniDbQuery.VAL_NM_RQ={VAL_NM_RQ}&UniDbQuery.From={From}&UniDbQuery.To={To}", где в фигурных скобках {} указывается отдельный параметр. Нас интересуют параметры VAL_NM_RQ, From и To.
Полученная информация по валютам вляется многомерным временным рядом (ВР). База данных будет SQLite3 и будет состоять из одной таблицы. Все показатели ВР будут заноситься в нее. Будем использовать ОРМ SQLAlchemy.

Для запуска проекта необходимо запустить скрипт run.py и следовать сообщениям

В планах еще создать приложение с "фронтом" на Vue3, модулем анализа ВР и запихнуть все в докер.
