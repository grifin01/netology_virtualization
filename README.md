# Домашнее задание к занятию 1.  «Введение в виртуализацию. Типы и функции гипервизоров. Обзор рынка вендоров и областей применения»

## Задача 1

Опишите кратко, в чём основное отличие полной (аппаратной) виртуализации, паравиртуализации и виртуализации на основе ОС.

## Ответ

-	Аппаратная (полная) виртуализация полностью имитирует оборудование для гостевой ОС. В итоге получается среда, аналогичная ОС, работающей на отдельном сервере. Использование полной виртуализации позволяет запускать виртуальные среды любых конфигураций без каких-либо дополнительных аппаратных решений.
-	Паравиртулизация – подход, при котором на виртуальной машине запускается особым образом подготовленная версия гостевой ОС, а выполнение привилегированных инструкций происходит через гипервизор. Таким образом происходит серьезное изменение ядра гостевой ОС.
-	Виртуализация на основе ОС (контейнеризация) – позволяет выделять новые пространства имен, ограничивать ресурсы хостовой машины, создавая изолированные контейнеры, в которых будут выполняться процессы. При этом ядро гостевой ОС не отличается от ядра хостовой ОС.

## Задача 2

Выберите один из вариантов использования организации физических серверов в зависимости от условий использования.

Организация серверов:

- физические сервера,
- паравиртуализация,
- виртуализация уровня ОС.

Условия использования:

- высоконагруженная база данных, чувствительная к отказу;
- различные web-приложения;
- Windows-системы для использования бухгалтерским отделом;
- системы, выполняющие высокопроизводительные расчёты на GPU.

Опишите, почему вы выбрали к каждому целевому использованию такую организацию.

## Ответ

1. Высоконагруженная база данных, чувствительная к отказу: виртуализация уровня ОС - в данном случае БД можно рассмотреть в качестве приложения, которое работает в нескольких "контейнерах", представляющих собой единый отказоустойчивый кластер. Администирование данных контейнеров проще, быстрее и не требует дополнительных расходов.
2. Различные web-приложения: виртуализация уровня ОС подойдет, если подразумевается, что приложения работают на том же ядре, что и ядро хостовой ОС. При наличии каких-либо ограничений я бы использовал паравиртуализацию. Web-приложениям свойственны частые обращения от клиентов, поэтому необходимо обеспечить должный уровень производительности, администрирование "контейнеров" позволяет упростить процесс управления самими веб-приложениями.
3. Windows-системы для использования бухгалтерским отделом: паравиртуализация - т.к. бухгалтерские системы, в основном, не требуют большой производительности, количество пользователей и частоту обращений можно спрогнозировать. Также при данном сценарии процессы миграции и создания резервных копий производятся легче.
4. Системы, выполняющие высокопроизводительные расчеты на GPU: физические сервера т.к. виртуализация может негативно влиять на эффективность использования вычислительных ресурсов. Отмечу наличие специализированных решений паравиртуализации, предназначенных для применения в данной области, но в данном случае производительность может пострадать.


