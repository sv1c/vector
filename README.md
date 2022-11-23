# **Vector_TechJournal.** Парсинг технологического журнала 1С


- [Назначение](#назначение)
    - [Возможности](#возможности)
- [Реализация](#реализация)
- [Запуск](#запуск)
- [План реализации](#Планы)
- [Лицензия](#лицензия)

## Назначение

Данный проект создан для того чтобы искоренить боль от использования технологического журнала.

Использование ТЖ должно свестись к трем простым действиям.
- Настроил ТЖ
- Запустил сборщик
- Приступил к анализу.

### Возможности

- Vector_TechJournal - это конфигурация Vector для разбора и трансформации файлов технологического журнала
- Предоставляет возможности чтения файлов  ТЖ
- В планах реализация разбора всех известных событий ТЖ.
- Выгрузка результатов парсинга в различных форматах
    - В файлы в различных форматах
    - В в консоль
    - В <b>Clickhouse</b>
    - В <b>Loki</b> и другие аггрегаторы логов 
- Возможность масштабирования решения в случае большего объема логов


## Реализация:

Продукт представлен в виде docker-compose файла и пригоден для запуска в любой среде поддерживающей контейнеры, а так же файлов конфигурации для него.
Конфигурация обработки каждого отдельного вида событий находится в <b>./config/transformations/\<EventName>.vrl</b>



## Запуск

Для запуска разбора технологического журнала достаточно:
- Подготовить базу данных clickhouse
    - Создать базу 
    - Создать таблицы скриптами из папки [sql_scripts](https://github.com/Segate-ekb/vector/tree/main/sql_scripts)
- Отредактировать файл techJournal.env
    - указать необходимые события которые вы планируете хранить
    - Задать параметры авторизации в Clickhouse
- В файле [docker-compose.yaml](https://github.com/Segate-ekb/vector/tree/main/sql_scripts) указать в Volume параметры подключения к папке с логами.   
- docker-compose up -d    

## Планы на ближайшее время
- Дописать разбор самых востребованых событий.
    - CALL
    - SCALL
    - и тд
- Отладить и оптимизировать разбор.
- Добавить словари для "Очеловечивания" информации
- Реализовать фронтенд для удобного просмотра и анализа ТЖ


---

## Лицензия

Distributed under the [Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.html)