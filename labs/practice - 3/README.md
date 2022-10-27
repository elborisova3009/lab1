## Практическая работа. 

![Практическая работа](https://user-images.githubusercontent.com/103572690/197572815-67ba936d-bf88-475e-90c1-1215f6b32e36.JPG)

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

LACP:

```
conf t
int range Fa0/4-5
channel-group 1 mode active
int port-channel 1
sw mode trunk
sw trunk alow vlan 1,10,99
```
PagP:

```
conf t
int range Fa0/6-7
channel-group 2 mode des
int port-channel 2
sw mode trunk
sw trunk alow vlan 1,10,99
```
* Проверяем правильность настройки Etherchannel: `sh etherchannel summary`
* Сохраняем конфигурацию в энергонезависимую память: `copy runn start`

# SW1

```
conf t
ip default-gateway 172.17.127.254
VLAN 99
name Managment
int Vlan 99
ip add 172.17.0.1 255.255.128.0
no shutdown
VLAN 10
name Workplaces
```
* Настраиваем порт для связи с маршрутизатором R1:
```
int g0/1
sw mod trunk
sw tr all vlan 10,1,99
```

* настраиваем транк для PagP Fa0/6-7 и Fa0/1-3 (no protocol)

PagP

```
int range Fa0/6-7
channel-group 2 mode desirable
interf port-channel 2
sw mode trunk
sw trunk allowed vlan 1,10,99
```
No protocol

```
int range Fa0/1-3
channel-group 3
channel-group 3 mode on
interf port-channel 3 
sw mode trunk
sw trunk allow vlan 1,10,99
```
* Проверяем правильность настройки Etherchannel: `sh etherchannel summary`
* Сохраняем конфигурацию в энергонезависимую память: `copy runn start`
* _Уже можно проверить ping до SW2_ `ping 172.17.0.2`

# SW3

```
conf t
ip default-gateway 172.17.127.254
VLAN 99
name Managment
interf Vlan 99
ip add 172.17.0.3 255.255.128.0
no shutdown
VLAN 10
name Workplaces
```
* Настраиваем порт для связи с маршрутизатором R1:

```
int g0/1
sw mod trunk
sw tr all vlan 10,1,99
```

* настраиваем транк для LACP Fa0/4-5 и Fa0/1-3 (no protocol)

LACP

```
int range Fa0/4-5
channel-group 1 mode active
interf port-channel 1
sw mode trunk
sw trunk allowed vlan 1,10,99
```
No protocol

```
int range Fa0/1-3
channel-group 3
channel-group 3 mode on
interf port-channel 3 
sw mode trunk
sw trunk allow vlan 1,10,99
```
* Проверяем правильность настройки Etherchannel: `sh etherchannel summary`
* Сохраняем конфигурацию в энергонезависимую память: `copy runn start`
* _Уже можно проверить ping до SW2_ `ping 172.17.0.2` _и 1:_ `ping 172.17.0.1`
</details> 

<details>
<summary>4. Настройка Роутеров R1 и R2</summary>

* a. Базовая настройка маршрутизаторов (Одинаковая для R1 и R0)
```
en
erase start
reload
en
conf t
hostname R1/0
no ip domain-lookup
conf t
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
clock set 21:58:35 24 sept 2022
```
* b. Настройка ip и подинтерфеса. И виртуального маршрутизатора HSRP v2
  
_Настраиваем R1:
* (Каждый сабинтерфейс+ HSRP)
```
conf t
int vlan 99
int vlan 10  
conf t
int g0/1
desc link to SW1
no shutdown  
interface GigabitEthernet0/0.1
description default gateway for DNS server
encapsulation dot1Q 1
ip address 10.0.0.2 255.255.255.0
standby 1 ip 10.0.0.6
standby 1 prior 200
standby 1 preempt  
interface GigabitEthernet0/1.10
description default gataway for vlan 10  
encapsulation dot1Q 10
ip add 192.168.10.124 255.255.255.128
standby 10 ip 192.168.10.126  
standby 10 priority 200
standby 10 preempt  
interface GigabitEthernet0/1.99
description default gataway for vlan99
encapsulation dot1Q 99
ip address 172.17.127.252 255.255.128.0
standby 99 ip 172.17.127.254
standby 99 prority 200
standby 99 preempt
exit  
copy runnyng startup  
```        
проверяем правильность настроек: `sh standby`
  
_На этом этапе уже можно проверить пинг до всех настроеных HSRP узлов_
  
# Настраиваем R0:
  
Базовые настройки + настройки Vlan, далее:
  
```
conf t
int g0/0.1
desc default gataway for DNS server
encap dot1Q 1
ip address 10.0.0.3 255.255.255.0 
standby 1 ip 10.0.0.6
standby 1 priority 100
exit
int g0/1.10
desc default gataway for vlan 10
enc dot1Q 10
ip add 192.168.10.125 255.255.255.128
standby 10 ip 192.168.10.126
standby 10 priority 100
exit
int g0/1.99
desc default router for managment
enc dot1Q 99
ip address 172.17.127.253 255.255.255.128
standby 99 ip 172.17.127.254
standby 99 prior 100
exit
copy runn start  
```  
#Вопросы к перподавателю:
_Как правильно пользоваться командой `standby 10 track G0/0` и как она связана с `standby 99 preempt` ?_
  
</details>
  
### Настраиваем Server-PT:
1. Настраиваем физический интерфейс:
* ip `10.0.0.1` маска подсети `255.255.255.0` шлюз: `10.0.0.6` dns `10.0.0.1`
1. Включаем DNS сервер `on` + добавляем "web странички": site.com
1.  Проверяем доступность страниц с PC и Laptop
