## Лабраторная работа - Настройка DHCP


<details><summary>1. Настройка DHCPv4</summary>
  
### Топология
  
  
  
  

   1. First item must be preceeded with an empty line.
   2. Markdown renders **perfectly**.
   1. Extra item.

</details>


<details><summary>1. Настройка DHCPv6</summary>

   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>


 
<details>
<summary>1. Настройка DHCPv4</summary> 
* а. настраиваем базовые параметры (одинаковые для каждого свитча `S2,S1,S3`)
  
<summary>2. Настройка DHCPv6</summary> 
* а. настраиваем базовые параметры (одинаковые для каждого свитча `S2,S1,S3`)


### План

1. Настройка ПК и ноутбука.
* а. Прописываем настройки в сетевые адаптеры "пользовательских" устройств. В качестве шлюза указываем адрес маршрутизатора из их же подстети: `192.168.10.126` В качестве ДНС сервера: адрес ДНС сервера из комментариев к ПР: `10.0.0.1`

<details>
<summary>3. Настройка Свитчей. Протоколы PagP и LACP</summary> 
* а. настраиваем базовые параметры (одинаковые для каждого свитча `S2,S1,S3`)
  
```
en
erase start
delete vlan.dat
conf t
no ip domain-lookup
enable secret class
line console 0
password cisco
login
logging synchronous
line vty 0 4
password cisco
login
^Z
conf t
banner motd 8 Achtung! 8
```
* b. Настраиваю VLAN 99 (управления) и VLAN 10 (Workplaces)

# SW2

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
* направляем "клиентские" порты во VLAN10:

```
int range Fa0/23, Fa0/24
sw mod acce
sw acce VLAN 10
^Z
```
* настраиваем транк для LACP Fa0/4-5 и PagP Fa0/6-7
  

  
<summary>2. Настройка DHCPv6</summary> 
* а. настраиваем базовые параметры (одинаковые для каждого свитча `S2,S1,S3`)
