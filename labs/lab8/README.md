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
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20115331-1.jpg)    
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
Шаг 5.	Настрою G0/0/1 на R2, затем G0/0/0 и статическую маршрутизацию для обоих маршрутизаторов.  
Базовую настройку R2 также проведу, но отражать в данной работе не буду.    
a.	Настрою G0/0/1 на R2 с первым IP-адресом подсети C, рассчитанным ранее.  
b.	Настрою интерфейс G0/0/0 для каждого маршрутизатора на основе приведенной выше таблицы IP-адресации.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20113703.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20113741.jpg)  
c.	Настрою маршрут по умолчанию на каждом маршрутизаторе, указывающий на IP-адрес G0/0/0 на другом маршрутизаторе.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20174832.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20174818.jpg)  
d.	Проверю, что статическая маршрутизация работает с помощью пинга до адреса G0/0/1 R2 от R1.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20174849.jpg)  
e.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  

Шаг 6.	Настрою базовые параметры каждого коммутатора по стандартному алгоритму:  
a.	Присвою коммутатору имя устройства.  
b.	Отключу поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначу class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначу cisco в качестве пароля консоли и включите вход в систему по паролю.  
e.	Назначу cisco в качестве пароля VTY и включите вход в систему по паролю.  
f.	Зашифрую открытые пароли.  
g.	Создам баннер с предупреждением о запрете несанкционированного доступа к устройству.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20125127.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20125150.jpg)   
h.	Установлю время.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20125710.jpg)  
i.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20125717.jpg)  
Примечание. S2 настроен аналогично.
  
Шаг 7.	Создам сети VLAN на коммутаторе S1.  
a.	Создам необходимые VLAN на S1 и присвою им имена из приведенной выше таблицы.  
b.	Настрою и активирую интерфейс управления на S1 (VLAN 200), используя второй IP-адрес из подсети, рассчитанный ранее.  
Кроме того, установлю шлюз по умолчанию на S1.  
_c.	Настрою и активирую интерфейс управления на S2 (VLAN 1), используя второй IP-адрес из подсети, рассчитанный ранее. 
Кроме того, установлю шлюз по умолчанию на S2._  
d.	Назначу все неиспользуемые порты S1 VLAN Parking_Lot, настрою их для статического режима доступа и административно деактивирую их.  
e.  На S2 административно деактивирую все неиспользуемые порты.  
S1:  
```
conf t
vlan 100
name Clients
int fa 0/6
no sh
sw m acc
sw ac vlan 100
exit
vlan 200
name Management
exit
interface vlan 200
ip address 192.168.1.66 255.255.255.224
no sh
exit
ip default-gateway 10.0.0.1
exit
vlan 999
name Parking_Lot
exit
int range fa 0/1-4, fa 0/7-24, gi 0/1-2
sw m acc
sw ac vlan 999
exit
vlan 999
shutdown
exit
vlan 1000
name Native
end
```  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20145543.jpg)   
S2:  
_Столкнулась со сложностью при выполнении раздела c. Шага 7.  
В начале работы для S2 не было задано рассчитать второй IP-адрес из подсети и указать шлюз по умолчанию. Задам их самостоятельно, по аналогии с S1, из подсети С.  
Теперь таблица адресации выглядит следующим олбразом._  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20153112.jpg)  
```  
configure terminal 
vlan 1
interface vlan 1
ip address 192.168.1.98 255.255.255.240
no sh
exit
ip default-gateway 10.0.0.2
int fa 0/18
no sh
sw m acc
sw ac vlan 1
exit
int range fa 0/1-4, fa 0/6-17, fa 0/19-24, gi 0/1-2
shutdown
end  
```  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20155802.jpg)  
  
Шаг 8. (был выполнен на предыдущем шаге)    
Сети VLAN были назначены соответствующим интерфейсам коммутаторов.
a.	Назначены используемые порты соответствующим VLAN (указанным в таблице VLAN выше) и настроены для режима статического доступа.  
b.	VLAN назначены на правильные интерфейсы:   
S1:  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2002-11-2022%20145330-1.jpg)   
Вопрос:  
Почему интерфейс fa 0/5 указан в VLAN 1? _Эти интерфейсы на S1 и S2 смотрят на роутеры. На S1 fa 0/5 должен быть настроен в качестве магистрального. Не могут быть административно выключены. Следовательно, остаются во VLAN 1._  

Шаг 9.	Вручную настрою интерфейс S1 F0/5 в качестве транка 802.1Q.
a.	Изменю режим порта коммутатора, чтобы принудительно создать магистральный канал.
b.	В рамках конфигурации транка  установлю для native  VLAN значение 1000.
c.	В качестве другой части конфигурации магистрали укажу, что VLAN 100, 200 и 1000 могут проходить по транку.
d.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.
  
```  
configure terminal    
interface fa 0/5   
switchport mode trunk   
switchport trunk native vlan 1000   
switchport trunk allowed vlan 100,200,1000   
switchport nonegotiate   
exit   
copy run start     
```  
e.	Проверю состояние транка.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-11-2022%20144114.jpg)    
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-11-2022%20144130.jpg)  
Вопрос:
Какой IP-адрес был бы у ПК, если бы он был подключен к сети с помощью DHCP? _Адрес был бы назначен автоматически из пула заданных при настройке DHCP адресов._  
  </details>   

<details><summary>Часть 2. Настройка и проверка двух серверов DHCPv4 на R1.</summary>  
На R1 сервер DHCPv4 будет обслуживать две подсети: подсеть A и подсеть C.

Шаг 1.	Настрою R1 с пулами DHCPv4 для поддерживаемых подсетей A и C.  
a.	Исключу первые пять используемых адресов из каждого пула адресов.  
b.	Создам пулы DHCP, используя уникальные имена для каждого пула: `POOL_A_R1_Client_LAN` и `POOL_C_R2_Client_LAN`.  
c.	Укажу сети, поддерживающие этот DHCP-сервер: `192.168.1.0 255.255.255.192` и `192.168.1.96 255.255.255.240`.  
d.	В качестве имени домена для двух подсетей укажу `CCNA-lab.com`.  
e.	Настрою соответствующие шлюзы по умолчанию для каждого пула DHCP: `192.168.1.1` и `192.168.1.98`.  
f.	Настрою время аренды двух пулов на 2 дня 12 часов и 30 минут. *Важно - CPT не поддерживает данную возможность*.
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2010-11-2022%20110511.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2010-11-2022%20110529.jpg)  

Шаг 2.	Сохраню конфигурацию.

Шаг 3.	Проверю конфигурации сервера DHCPv4.  
a.	Сведения о пуле: `show ip dhcp pool`.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2010-11-2022%20170131.jpg)  
b.	Установленные назначения адресов DHCP: `show ip dhcp binding`.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2010-11-2022%20170315.jpg)  
c.	Сообщения DHCP: `show ip dhcp server statistics`.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2010-11-2022%20170440.jpg)  

Шаг 4.	Попытка получить IP-адрес от DHCP на PC-A.  
a.	Из командной строки компьютера PC-A выполню команду ipconfig /all.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20140235.jpg)  
b.	После завершения процесса обновления выполните команду ipconfig для просмотра новой информации об IP-адресе.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20140331.jpg)  
c.	Проверьте подключение с помощью пинга IP-адреса интерфейса R0 G0/0/1.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20140539.jpg)  

</details>

<details><summary>Часть 3. Настройка и проверка DHCP-ретрансляции на R2.</summary>    
В этой части R2 будет настроен для ретрансляции DHCP-запросов из локальной сети на интерфейсе G0/0/1 на DHCP-сервер (R1).   
Шаг 1.	Настройка R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.  
a.	Настройте команду ip helper-address на G0/0/1, указав IP-адрес G0/0/0 R1.  
b.	Сохраните конфигурацию.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20153445.jpg)

Шаг 2.	Попытка получить IP-адрес от DHCP на PC-B.  
a.	Из командной строки компьютера PC-B выполните команду ipconfig /all.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20155801.jpg)  
b.	После завершения процесса обновления выполните команду ipconfig для просмотра новой информации об IP-адресе.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20155821.jpg)  
c.	Проверьте подключение с помощью пинга IP-адреса интерфейса R1 G0/0/1 *Пинга нет, утрата логики, где IP-адрес интерфейса R1 G0/0/1???*.  
d.	Выполните show ip dhcp binding для R1 для проверки назначений адресов в DHCP.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20160423.jpg)  
e.	Выполните команду show ip dhcp server statistics для проверки сообщений DHCP.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-11-2022%20160548.jpg)  

  </details>

