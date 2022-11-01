## Лабораторная работа - Настройка DHCP


<details><summary>1. Настройка DHCPv4</summary>
  
### Топология

![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20132045.jpg)  

### Таблица адресации
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20135251.jpg)
  
###	Таблица VLAN
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20135429.jpg)  
  
###	Задачи

<details><summary>Часть 1. Создание сети и настройка основных параметров устройства.  </summary>

  Шаг 1.	Оформлю схему адресации.    
Задам подсеть сети 192.168.1.0/24 в соответствии со следующими требованиями:
  
a.	Одна подсеть «Подсеть A», поддерживающая 58 хостов (клиентская VLAN на R1).  
Подсеть A:  
Запишу первый IP-адрес в таблице адресации для R1 G0/0/1.100.
  
b.	Одна подсеть «Подсеть B», поддерживающая 28 хостов (управляющая VLAN на R1).  
Подсеть B:  
Запишу первый IP-адрес в таблице адресации для R1 G0/0/1.200.  
Запишу второй IP-адрес в таблице адресов для S1 VLAN 200, укажу соответствующий шлюз по умолчанию.
  
c.	Одна подсеть «Подсеть C», поддерживающая 12 узлов (клиентская сеть на R2).  
Подсеть C:  
Запишу первый IP-адрес в таблице адресации для R2 G0/0/1.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20115331.jpg)  
  
Шаг 2.	Создам в CPT сеть согласно топологии.
  
Шаг 3.	Произведу базовую настройку маршрутизаторов.  
  ```
enable
configure terminal
hostname R1
no ip domain lookup
enable secret class
line console 0
password cisco
login
exit
line vty 0 4
password cisco
login
exit
service password-encryption
banner motd #UNAUTHORIZED ACCESS PROHIBITED, GO AWAY!#
exit
copy run start
show run
clock set 13:30:00 Nov 01 2022
show clock  
```
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20131511.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20141911.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20141925.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20141945.jpg)  
  
Шаг 4.	Настрою маршрутизацию между сетями VLAN на маршрутизаторе R1.    
a.	Активирую интерфейс G0/0/1.  
b.	Настрою подинтерфейсы для каждой VLAN в соответствии с требованиями таблицы IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q.  
Проверю, что подинтерфейсу для native VLAN не назначен IP-адрес.  
Включу описание для каждого подинтерфейса.  
c.	Проверю, что подинтерфейсы работают.   
```
conf t
int gi 0/0/1
no shutdown
exit
int gi 0/0/1.100
description Clients
encapsulation dot1q 100
ip address 192.168.1.1 255.255.255.192
no shutdown
exit
int gi 0/0/1.200
description Management
encapsulation dot1q 200
ip address 192.168.1.65 255.255.255.224
no shutdown
exit
int gi 0/0/1.1000
description Native
encapsulation dot1q 2
no shutdown
end
```  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20141404.jpg)  

Шаг 5.	Настрою G0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов (базовую настройку также проведу, но отражать в данной не буду).  
a.	Настрою G0/0/1 на R2 с первым IP-адресом подсети C, рассчитанным ранее.  
b.	Настрою интерфейс G0/0/0 для каждого маршрутизатора на основе приведенной выше таблицы IP-адресации.  
c.	Настрою маршрут по умолчанию на каждом маршрутизаторе, указываемом на IP-адрес G0/0/0 на другом маршрутизаторе.  
d.	Проверю, что статическая маршрутизация работает с помощью пинга до адреса G0/0/1 R2 от R1.  
e.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
  
  
  


  
  

  
</details>   

  
  
  ### Настраиваем Server-PT:
1. Настраиваем физический интерфейс:
* ip `10.0.0.1` маска подсети `255.255.255.0` шлюз: `10.0.0.6` dns `10.0.0.1`
1. Включаем DNS сервер `on` + добавляем "web странички": site.com
1.  Проверяем доступность страниц с PC и Laptop
  


<details><summary>Часть 2. Настройка и проверка двух серверов DHCPv4 на R1</summary>  

   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>

<details><summary>Часть 3. Настройка и проверка DHCP-ретрансляции на R2.</summary> 


   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>
  
    1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

  

</details>

_____________________________________


<details><summary>2. Настройка DHCPv6</summary>

   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>

_____________________________________


```
conf t
ip default-gateway 172.17.127.254
VLAN 99
name Managment
int Vlan 99
ip add 172.17.0.2 255.255.128.0
no shutdown
VLAN 10
name Workplaces
```

