## Лабораторная работа 4. Настройка IPv6-адресов на сетевых устройствах 
### Топология
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20180809.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20014751.jpg)  
### 	Таблица адресации
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20181153.jpg)  
### 	Задачи
Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора  
Часть 2. Ручная настройка IPv6-адресов  
Часть 3. Проверка сквозного соединения  

### 	Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора

Шаг 1. Настройка маршрутизатора. Назначение имени хоста и настройка основных параметров устройства.  
Конфигурация:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20183345.jpg)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20184825.jpg)

Шаг 2. Настройка коммутатора. Назначение имени хоста и настройка основных параметров устройства.  
Конфигурация:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20185607.jpg)

### 	Часть 2. Ручная настройка IPv6-адресов

Шаг 1. Назначаю IPv6-адреса интерфейсам Ethernet на R1.    
a.	В командной строке на PC-B ввожу команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу компьютера.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20190610.jpg)  
b.	Ввожу команду show ipv6 interface brief, чтобы проверить, назначен ли каждому интерфейсу действительный IPv6-адрес одноадресной передачи.  
(Отображаемый локальный адрес канала основан на адресации EUI-64, которая автоматически использует MAC-адрес интерфейса для создания 128-битного локального IPv6-адреса канала.)   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20190947.jpg)  
Вижу искомые адреса:      
GigabitEthernet0/0    
2001:DB8:ACAD:A::1    
GigabitEthernet0/1    
2001:DB8:ACAD:1::1    
c.	Ввожу команду show ipv6 interface g0/0. Учитываю, что в интерфейсе содержатся две многоадресные группы запрошенных узлов, поскольку идентификатор интерфейса локального канала (FE80) IPv6-адреса не был настроен в соответствии с идентификатором интерфейса IPv6-адреса одноадресной передачи вручную.  
Обращаю внимание:    
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20193610.jpg)   
d.	Чтобы локальный адрес канала соответствовал адресу одноадресной передачи в интерфейсе, вручную ввожу локальные адреса каналов для каждого из двух Ethernet-интерфейсов маршрутизатора R1. (Каждый интерфейс маршрутизатора относится к отдельной сети. Пакеты с локальным адресом канала никогда не выходят за пределы локальной сети, а значит, для обоих интерфейсов можно указывать один и тот же локальный адрес канала.)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20194333.jpg)  
e. Еще раз ввожу команду show ipv6interface g0/0. Учитываю, что локальный адрес канала изменился на FE80::1 и осталась только одна многоадресная группа запрошенных узлов.    
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20221506.jpg)  
Вопрос.  
Какие многоадресные группы назначены интерфейсу G0/0?  
FF02::1  

Шаг 2. Активирую IPv6-маршрутизацию на R1.    
a.	В командной строке на PC-B ввожу команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу компьютера.   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20232305.jpg)   
Вопрос:  
Назначен ли индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) на PC-B?  
Нет, не назначен.    
b.	Активирую IPv6-маршрутизацию на R1 с помощью команды IPv6 unicast-routing - это позволит компьютерам получать IP-адреса и данные шлюза по умолчанию с помощью функции SLAAC (Stateless Address Autoconfiguration (Автоконфигурация без сохранения состояния адреса)).  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20232618.jpg)  
Новая многоадресная группа назначена интерфейсу G0/0/0 - теперь в списке групп для интерфейса G0/0 отображается группа многоадресной рассылки всех маршрутизаторов (FF02::2).  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20233255.jpg)  
c.	Теперь, когда R1 входит в группу многоадресной рассылки всех маршрутизаторов, еще раз ввожу команду ipconfig на PC-B. Проверяю данные IPv6-адреса.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2007-10-2022%20234638.jpg)  
Вопрос:  
Почему PC-B получил глобальный префикс маршрутизации и идентификатор подсети, которые я настроила на R1?  
Потому, что PC-B получает свой IPv6-адреса и шлюз по умолчанию через SLAAC.  

Шаг 3. Назначаю IPv6-адреса интерфейсу управления (SVI) на S1.  
a.	Назначаю полученный IPv6-адрес интерфейсу управления (в данной работе я вынесла SVI во VLAN 2) на коммутаторе S1. Также назначу этому интерфейсу локальный адрес канала. Аналогично, как и на маршрутизаторе. *Но! Важно учесть - на коммутаторе должен быть задан свой локальный адрес канала.*  
Для начала установилю шаблон dual-ipv4-and-ipv6 в качестве шаблона SDM по умолчанию, а затем выполню следующие действия:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20012114.jpg)  
Затем определю порты fa 0/5 и fa 0/6 во VLAN 2, переведу соотвутствующие порты в режимы acess и trunk.    
После чего перейду к назначению IPv6 адресов согласно заданию.   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20012955-1.jpg)   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20111418.jpg)  
b.	Проверю правильность назначения IPv6-адресов интерфейсу управления с помощью команды show ipv6 interface vlan2.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20111830.jpg)  

Шаг 4. Назначу компьютерам статические IPv6-адреса.    
На реальном железе:   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20013857.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20013908.jpg)  
В CPT:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20015134.jpg)    
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20015114.jpg)   
Оба компьютера имеют правильную информацию адреса IPv6 - по два глобальных адреса IPv6: один статический и один SLACC. 


### Часть 3. Проверка сквозного подключения

С PC-A отправлю эхо-запрос на FE80::1 (локальный адрес канала, назначенный G0/1 на R1):  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20035721.jpg)  
С PC-A отправлю эхо-запрос на интерфейс управления S1:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20035346.jpg)  
Введу команду tracert на PC-A, чтобы проверить наличие сквозного подключения к PC-B:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20040106.jpg)  
С PC-B отправлю эхо-запрос на PC-A:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20040246.jpg)  
С PC-B отправлю эхо-запрос на FE80::1 (локальный адрес канала, назначенный G0/0 на R1):  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20040437.jpg)

### Вопросы для повторения  
1.	Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?  
Каждый интерфейс маршрутизатора находится в отдельной сети, а пкеты с локальным адресом канала никогда не покидают локальную сеть.  

2.	Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?  
0 (ноль) или 0000 (нули). В этом примере четвертый гекстет — это идентификатор подсети IPv6-адреса с префиксом /64.  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab4/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2008-10-2022%20041451.jpg)

