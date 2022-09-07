## Лабораторная работа 1. Базовая настройка коммутатора
### Топология

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(10-17-22).png?raw=true)
### 	Таблица адресации
![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(10-38-32).png)
### 	Задачи 

<a href="#1"> Часть 1. Создать сеть согласно топологии и проверить конфигурацию коммутатора по умолчанию </a>  

<a href="#2"> Часть 2. Настроить базовые параметры сетевых устройств </a>  
- Настроить базовые параметры коммутатора  
- Настроить IP-адрес для ПК  

<a href="#3"> Часть 3. Проверить сетевые подключения </a>
- Отобразить конфигурацию устройства  
- Протестировать сквозное соединение, отправив эхо-запрос  
- Протестировать возможности удаленного управления с помощью Telnet  

### 	Ход выполнения 

<a name="1"> Часть 1. Создать сеть согласно топологии и проверить конфигурацию коммутатора по умолчанию </a>
  
a. Создаем сеть согласно заданной топологии (Cisco PT, в доступе есть реальное оборудование). Устанавливаем консольное подключение между коммутатором S1 и компьютером PC-A. На данном этапе не подключаем кабель Ethernet. При первоначальной настройке коммутатора невозможно подключиться через Telnet или SSH - они используются, когда настраиваемое оборудование уже доступно по сети (как минимум у коммутатора на int vlan задан ip адрес, на vty линии активирован прикладной протокол удаленного доступа и тип аутентификации).   
![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(11-38-01).png)  
Проверяем конфигурацию коммутатора по умолчанию: текущие настройки коммутатора, данные IOS, свойства интерфейса, сведения о VLAN и флеш-память.

b. Изучим текущий файл running configuration.  

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(12-28-57).png) 

*Вопросы:*  

Сколько интерфейсов FastEthernet имеется на коммутаторе 2960? *24*     
Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960? *2*    
Каков диапазон значений, отображаемых в vty-линиях? *0-15*

c. Изучим файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM). 

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(14-32-42).png)

*Вопрос:* 

Почему появляется сообщение: startup-config is not present?  
*Типичное сообщение, когда коммутатор конфигурируется впервые (конфиг еще не записан) или сброшен к заводским настройкам. Никто еще не делал запись конфига.*

d. Изучим характеристики SVI для VLAN 1.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(14-29-02).png)

*Вопросы:* 

Назначен ли IP-адрес сети VLAN 1? *Нет.*    
Какой MAC-адрес имеет SVI? Возможны различные варианты ответов.  
*SVI не имеет MAC-адрес, MAC-адрес аппаратного интерфейса 00d0.d301.63bd*   
Данный интерфейс включен? *Выключен.*  

e. Изучим IP-свойства интерфейса SVI сети VLAN 1. 

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(14-38-46).png)

*Вопрос:* 
Какие выходные данные вы видите?  
*Интерфейс VLAN 1 выключен, IP-адрес для него не назначен, ни один из портов сети VLAN 1 не назначен.*

f. Подсоединим кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучим IP-свойства интерфейса SVI сети VLAN 1.   
Дождемся согласования параметров скорости и дуплекса между коммутатором и ПК.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(15-41-21).png)

*Вопрос:* 
Какие выходные данные вы видите?  
*Интерфейс VLAN 1 выключен, IP-адрес для него не назначен, ни один из портов сети VLAN 1 не назначен.*

g.	Изучим сведения о версии ОС Cisco IOS на коммутаторе.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(15-50-24).png)
![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(15-50-44).png)

*Вопросы:* 
Под управлением какой версии ОС Cisco IOS работает коммутатор? *Version 15.0(2)SE4*  
Как называется файл образа системы? *c2960-lanbasek9-mz.150-2.SE4.bin*   
Какой базовый MAC-адрес назначен коммутатору? *Base ethernet MAC Address: 00:D0:D3:01:63:BD*  

h.	Изучим свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(15-57-38).png) 

*Вопросы:* 
Интерфейс включен или выключен? *Включен* 
Что нужно сделать, чтобы включить интерфейс? *На коммутаторах порты по умолчанию включены.*  
Какой MAC-адрес у интерфейса? *0001.42de.3d06 (bia 0001.42de.3d06)* 
Какие настройки скорости и дуплекса заданы в интерфейсе? *Full-duplex, 100Mb/s*  

i.	Изучим параметры сети VLAN по умолчанию на коммутаторе.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(16-31-43).png)

*Вопросы:* 
Какое имя присвоено сети VLAN 1 по умолчанию? *default*  
Какие порты расположены в сети VLAN 1? *Все.*  
Активна ли сеть VLAN 1? *Да.*
К какому типу сетей VLAN принадлежит VLAN по умолчанию? *enet*

j.	Изучим флеш-память.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(16-37-47).png)

*Вопрос:*
Какое имя присвоено образу Cisco IOS? *2960-lanbasek9-mz.150-2.SE4.bin*


 <a name="2"> Часть 2. Настроить базовые параметры сетевых устройств </a>
 
- Настроить базовые параметры коммутатора

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_06.09.2022(17-53-48).png)

- Настроить IP-адрес для ПК  

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(13-13-15).png)
 
 <a name="3"> Часть 3. Проверить сетевые подключения </a>
 
Шаг 1. Отобразим конфигурацию коммутатора.

a.	Отобразим текущую конфигурацию. 

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-46-07).png)

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-46-28).png)

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-46-57).png)

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-47-45).png)

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-48-12).png)

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-49-02).png)

b. Проверим параметры VLAN 1.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-58-31).png)

*Вопросы:* 
Какова полоса пропускания этого интерфейса? - *BW 100000 Kbit*   
В каком состоянии находится VLAN 1? - *Vlan1 is administratively down*  
В каком состоянии находится канальный протокол? - *Vlan1 is administratively down*  

b-1. Факультативно. Проверим параметры VLAN 77.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(12-58-31).png)

*Вопросы:* 
Какова полоса пропускания этого интерфейса? - *BW 100000 Kbit*   
В каком состоянии находится VLAN 77? - *Vlan77 is up*  
В каком состоянии находится канальный протокол? - *line protocol is up*  

Шаг 2. Протестируем сквозное соединение, отправив эхо-запрос.

a.	C:\> ping 192.168.1.10 

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(13-17-12).png)

b.	C:\> ping 192.168.1.2 (эхо-запрос на административный адрес интерфейса SVI коммутатора S1).

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(13-17-12).png)

Шаг 3. Проверим удаленное управление коммутатором S1.

![alt text](https://github.com/elborisova3009/otus-network-engineer/blob/main/Screenshot_07.09.2022(13-56-27).png)

### 	Вопросы для повторения

1.	Зачем необходимо настраивать пароль VTY для коммутатора? *Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet (в нашем случае). VTY - виртуальный интерфейс, обеспечивающий удаленный доступ.*  
2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде? *Применить команду enable secret, которая обеспечивает бОльшую безопасность (по сравнению с enable password) - шифруя пароль.*













 
 
 


