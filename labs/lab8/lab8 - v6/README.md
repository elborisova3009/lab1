## Лабораторная работа - Настройка DHCP 

<details><summary>2. Настройка DHCP. Реализация DHCPv6 </summary>
  
### Топология

![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20132045.jpg)  

### Таблица адресации
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2017-11-2022%20110014.jpg)
  
###	Задачи
  
  ###	Задачи

<details><summary>Создание сети и настройка основных параметров устройства.  </summary>

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
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20174623.jpg)  
Шаг 2.	Создам в CPT сеть согласно топологии.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20175036.jpg)  
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

  </details>   
  

  <details><summary>Создание сети и настройка основных параметров устройства.  </summary>

 Часть 2. Проверка назначения адреса SLAAC от R1

  </details>   
  
 Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1

  </details>   
  
Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1
Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1
Часть 5. Настройка и проверка DHCPv6 Relay на R2

  
  
  
