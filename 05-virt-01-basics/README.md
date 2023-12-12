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
3. Windows-системы для использования бухгалтерским отделом: паравиртуализация, т.к. бухгалтерские системы, в основном, не требуют большой производительности, количество пользователей и частоту обращений можно спрогнозировать. Также при данном сценарии процессы миграции и создания резервных копий производятся легче.
4. Системы, выполняющие высокопроизводительные расчеты на GPU: физические сервера, т.к. виртуализация может негативно влиять на эффективность использования вычислительных ресурсов. Отмечу наличие специализированных решений паравиртуализации, предназначенных для применения в данной области, но в данном случае производительность может пострадать.

## Задача 3

Выберите подходящую систему управления виртуализацией для предложенного сценария. Детально опишите ваш выбор.

Сценарии:

1. 100 виртуальных машин на базе Linux и Windows, общие задачи, нет особых требований. Преимущественно Windows based-инфраструктура, требуется реализация программных балансировщиков нагрузки, репликации данных и автоматизированного механизма создания резервных копий.
2. Требуется наиболее производительное бесплатное open source-решение для виртуализации небольшой (20-30 серверов) инфраструктуры на базе Linux и Windows виртуальных машин.
3. Необходимо бесплатное, максимально совместимое и производительное решение для виртуализации Windows-инфраструктуры.
4. Необходимо рабочее окружение для тестирования программного продукта на нескольких дистрибутивах Linux.

## Ответ

1. VMWare. В рамках продуктов виртуализации и управления, решения от VMWare являются наиболее сбалансированными, имеют достаточно обширный функционал, который позволит закрыть вопросы по сопровождению и администрированию среды на 100 VM Windows и Linux. При наличии большого количества Windows-машин возможно использовать Hyper-V, ввиду лучшей совместимости.
2. Xen, KVM или Proxmox VE. Подойдут разные системы, в зависимости от выполняемых операций, т.к. разные виды задач требуют разный уровень производительности.
3. Microsoft Hyper-V имеет наибольшую совместимость с Windows-системами. В качестве альтернативного варианта можно использовать или Xen.
4. Решения виртуализации на уровне ОС, например, Docker позволяют получить наибольшую скорость развёртывания нескольких окружений для тестирования продукта.

## Задача 4

Опишите возможные проблемы и недостатки гетерогенной среды виртуализации (использования нескольких систем управления виртуализацией одновременно) и что необходимо сделать для минимизации этих рисков и проблем. Если бы у вас был выбор, создавали бы вы гетерогенную среду или нет? Мотивируйте ваш ответ примерами.

## Ответ

Перед окончательным выбором той или иной среды виртуализации должен быть сделан глубокий анализ инфраструктуры и задач, которые требуется выполнять в будущем. Считается, что лучше всего не разводить "зоопарк" из решений от разных вендоров по управлению виртуальной средой. Однако, допускается создание гетерогенной срелы с двумя или более решениями, если это будет опрадывать выполняемые в будущем задачи, как с точки зрения финансовой составляющей, так и администрирования. Следует учесть, что такой сценарий потребует наличие наиболее квалифицированного инженерного состава, готового выполнять большой объем работ с использованием элементов автоматизации под разные решения. Также для гетерогенной среды усложняется выбор решений для мониторинга и обеспечения отказоустойчивости. Помимо вышесказанного, усложняется вопрос доставки изменений в ту или иную среду. Как и для любого другого решения в инфраструктуре, в целях обеспечения доступности необходимо проработать план аварийно-восстановительных работ для всех систем управления виртуализацией. Как итог, гетерогенную среду можно использовать - главное серьезно подойти к вопросам планирования и реализации проекта, а также кадрового состава.