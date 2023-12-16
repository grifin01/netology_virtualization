# Домашнее задание к занятию 2. «Применение принципов IaaC в работе с виртуальными машинами»

## Задача 1

1. Опишите основные преимущества применения на практике IaaC-паттернов.
2. Какой из принципов IaaC является основополагающим?

## Ответ

1. Применение IaaC-паттернов значительно ускоряет процесс разворачивания необходимой инфраструктуры, что позволяя сделать быстрый откат изменений. Также появляется возможность тестирование продукта и оперативного внесения документированных корректировок в конфигурацию.
2. Основополагающим принципом IaaC является идемпотентность - свойство объекта или операции при повторном применении операции к объекту давать тот же результат, что и при первом.


## Задача 2

1. Чем Ansible выгодно отличается от других систем управление конфигурациями?2
2. Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?

## Ответ

1. Преимущества использования Ansible:
   * Безагентная установка и развертывание;
   * Доставка конфигураций по SSH;
   * Низкие накладные расходы;
   * Использование Python для разработки данной системы;
   * Простота в освоении.

3. Push: считается более надежным для обеспечения своевременных обновлений. Подходит для сценариев, где критичны мгновенные и синхронизированные изменения.
   Pull: подходит для сценариев, где низкая нагрузка на сеть и децентрализованное управление приоритетнее всего. Менее надежен в ситуациях, где критичны мгновенные обновления.

Выбор между push и pull зависит от конкретных потребностей системы, учитывая такие факторы, как состояние сети, требования ко времени выполнения и уровень контроля. Часто используется комбинированный подход, включающий оба метода.


## Задача 3

Установите на личный linux-компьютер(или учебную ВМ с linux):

- [VirtualBox](https://www.virtualbox.org/),
- [Vagrant](https://github.com/netology-code/devops-materials), рекомендуем версию 2.3.4(в более старших версиях могут возникать проблемы интеграции с ansible)
- [Terraform](https://github.com/netology-code/devops-materials/blob/master/README.md)  версии 1.5.Х (1.6.х может вызывать проблемы с яндекс-облаком),
- Ansible.

*Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.*

## Ответ

* VirtualBox:
```
vish@DevOps:~$ VBoxManage --version
7.0.12r159484
```

* Vagrant:
```
vish@DevOps:~$ vagrant -v
Vagrant 2.3.4
```

* Terraform:
```
vish@DevOps:~$ terraform -v
Terraform v1.6.6
on linux_amd64
```

* Ansible:
```
vish@DevOps:~$ ansible --version

ansible [core 2.15.8]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/vish/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  ansible collection location = /home/vish/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/bin/ansible
  python version = 3.10.12 (main, Nov 20 2023, 15:14:05) [GCC 11.4.0] (/usr/bin/python3)
  jinja version = 3.0.3
  libyaml = True
```

## Задача 4 

Воспроизведите практическую часть лекции самостоятельно.

- Создайте виртуальную машину.
- Зайдите внутрь ВМ, убедитесь, что Docker установлен с помощью команды
```
docker ps,
```
Vagrantfile из лекции и код ansible находятся в [папке](https://github.com/netology-code/virt-homeworks/tree/virt-11/05-virt-02-iaac/src).

Примечание. Если Vagrant выдаёт ошибку:
```
URL: ["https://vagrantcloud.com/bento/ubuntu-20.04"]     
Error: The requested URL returned error: 404:
```

выполните следующие действия:

1. Скачайте с [сайта](https://app.vagrantup.com/bento/boxes/ubuntu-20.04) файл-образ "bento/ubuntu-20.04".
2. Добавьте его в список образов Vagrant: "vagrant box add bento/ubuntu-20.04 <путь к файлу>".
