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


## Ответ

Создадим виртуальную машину:
```
vish@DevOps:~/Netology/devops-netology/vagrant_configs$ vagrant up
Bringing machine 'server1.netology' up with 'virtualbox' provider...
==> server1.netology: Importing base box 'bento/ubuntu-20.04'...
==> server1.netology: Matching MAC address for NAT networking...
==> server1.netology: Checking if box 'bento/ubuntu-20.04' version '202309.09.0' is up to date...
==> server1.netology: Setting the name of the VM: server1.netology
==> server1.netology: Clearing any previously set network interfaces...
==> server1.netology: Preparing network interfaces based on configuration...
    server1.netology: Adapter 1: nat
    server1.netology: Adapter 2: hostonly
==> server1.netology: Forwarding ports...
    server1.netology: 22 (guest) => 20011 (host) (adapter 1)
    server1.netology: 22 (guest) => 2222 (host) (adapter 1)
==> server1.netology: Running 'pre-boot' VM customizations...
==> server1.netology: Booting VM...
==> server1.netology: Waiting for machine to boot. This may take a few minutes...
    server1.netology: SSH address: 127.0.0.1:2222
    server1.netology: SSH username: vagrant
    server1.netology: SSH auth method: private key
    server1.netology: Warning: Connection reset. Retrying...
    server1.netology: Warning: Remote connection disconnect. Retrying...
    server1.netology: Warning: Connection reset. Retrying...
    server1.netology: Warning: Remote connection disconnect. Retrying...
    server1.netology: 
    server1.netology: Vagrant insecure key detected. Vagrant will automatically replace
    server1.netology: this with a newly generated keypair for better security.
    server1.netology: 
    server1.netology: Inserting generated public key within guest...
    server1.netology: Removing insecure key from the guest if it's present...
    server1.netology: Key inserted! Disconnecting and reconnecting using new SSH key...
==> server1.netology: Machine booted and ready!
==> server1.netology: Checking for guest additions in VM...
==> server1.netology: Setting hostname...
==> server1.netology: Configuring and enabling network interfaces...
==> server1.netology: Mounting shared folders...
    server1.netology: /vagrant => /home/vish/Netology/devops-netology/vagrant_configs
==> server1.netology: Running provisioner: ansible...
    server1.netology: Running ansible-playbook...
PLAY [nodes] *******************************************************************
TASK [Gathering Facts] *********************************************************
ok: [server1.netology]
TASK [Create directory for ssh-keys] *******************************************
ok: [server1.netology]
TASK [Adding rsa-key in /root/.ssh/authorized_keys] ****************************
changed: [server1.netology]
TASK [Checking DNS] ************************************************************
changed: [server1.netology]
TASK [Installing tools] ********************************************************
ok: [server1.netology] => (item=git)
ok: [server1.netology] => (item=curl)
TASK [Installing docker] *******************************************************
changed: [server1.netology]
TASK [Add the current user to docker group] ************************************
changed: [server1.netology]
PLAY RECAP *********************************************************************
server1.netology           : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 
```

Покдлючимся к ВМ по SSH:
```
vish@DevOps:~/Netology/devops-netology/vagrant_configs$ vagrant ssh
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.4.0-162-generic x86_64)
 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
  System information as of Sat 16 Dec 2023 05:12:24 PM UTC
  System load:  0.24               Users logged in:          0
  Usage of /:   14.0% of 30.34GB   IPv4 address for docker0: 172.17.0.1
  Memory usage: 31%                IPv4 address for eth0:    10.0.2.15
  Swap usage:   0%                 IPv4 address for eth1:    192.168.56.11
  Processes:    141
This system is built by the Bento project by Chef Software
More information can be found at https://github.com/chef/bento
Last login: Sat Dec 16 17:09:34 2023 from 10.0.2.2
```

Проверим, что Docker успешно установлен:
```
vagrant@server1:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

