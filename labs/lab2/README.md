## Лабораторная работа 2. Просмотр таблицы MAC-адресов коммутатора
### Топология
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(11-07-50).png)
### 	Таблица адресации
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(11-44-37).png)
### 	Цели 
<a href="#1"> Часть 1. Создание и настройка сети </a>  
<a href="#2"> Часть 2. Изучение таблицы МАС-адресов коммутатора </a>  
### 	Ход выполнения 

<a name="1"> Часть 1. Создание и настройка сети </a>
  
Шаг 1. В Cisco PT подключаем сеть в соответствии с топологией  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(12-20-58-).png)  

Шаг 2. Настраиваем узлы PC-A и PC-B - присваиваем им ip адреса, согласно таблице адресации.
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(12-38-28).png)
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(12-38-51).png)

Шаг 3. В Cisco PT выполнять инициализацию и перезагрузку коммутаторов не требуется. 

Алгоритм действий на живом железе следующий.      
Подключаемся к коммутатору с помощью консольного кабеля:  
Switch> enable    
Switch#  
Switch# show flash *(определяем, были ли созданы сети VLAN на коммутаторе)*   
Switch# delete vlan.dat *(если во флеш-памяти обнаружен файл vlan.dat, удаляем его)*    
Delete filename [vlan.dat]? *(запрос о проверке имени файла)*  
Delete flash:/vlan.dat? [confirm] *(запрос о подтверждении удаления этого файла)*  
Switch#    
Switch# erase startup-config  
Erasing the nvram filesystem will remove all configuration files! Continue? [confirm] [OK]    
Erase of nvram: complete  
Switch#  
Switch# reload  
Proceed with reload? [confirm] *(перезагрузка для удаления устаревшей информации о конфигурации из памяти, запрос о подтверждении перезагрузки коммутатора)*  
System configuration has been modified. Save? [yes/no]: no *(возможен запрос о сохранении текущей конфигурации перед перезагрузкой коммутатора)*     
Would you like to enter the initial configuration dialog? [yes/no]: no *(после перезагрузки коммутатора появится запрос о входе в диалоговое окно начальной конфигурации)*    
Switch>  

Шаг 4. Настраиваем базовые параметры каждого коммутатора.
  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(13-35-44).png)
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-10-52).png)


 <a name="2"> Часть 2. Изучение таблицы МАС-адресов коммутатора </a>
 
 a.	Открыть командную строку на PC-A и PC-B и ввести команду ipconfig /all  
 
 ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-32-27).png)
 ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-33-22).png)
 
  Физические адреса адаптера Ethernet:  
  PC-A: Physical Address................: 0030.F2E3.DD44  
  PC-B: Physical Address................: 000B.BEE9.18AC
  
  MAC-адрес компьютера PC-A: 0030.F2E3.DD44  
  MAC-адрес компьютера PC-B: 000B.BEE9.18AC  
  
  b.	Подключиться к коммутаторам S1 и S2 и ввести команду show interface F0/1 на каждом коммутаторе
  
  ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-58-41).png)
  ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-58-04).png)
  
  Адреса оборудования во второй строке выходных данных команды (или зашитый адрес — bia):
  
  МАС-адрес коммутатора S1 Fast Ethernet 0/1: address is 000c.cfa0.5401 (bia 000c.cfa0.5401)  
  МАС-адрес коммутатора S2 Fast Ethernet 0/1: address is 0000.0cc8.7001 (bia 0000.0cc8.7001)
  
  
  

  
  
  
  
  
  
 
 
 
 
 
 
 
 
 
 
- Настроить базовые параметры коммутатора

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_06.09.2022(17-53-48).png)

- Настроить IP-адрес для ПК  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(13-13-15).png)
 
 <a name="3"> Часть 3. Проверить сетевые подключения </a>
 
Шаг 1. Отобразим конфигурацию коммутатора.

a.	Отобразим текущую конфигурацию. 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-46-07).png)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-46-28).png)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-46-57).png)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-47-45).png)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-48-12).png)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-49-02).png)

b. Проверим параметры VLAN 1 (77) (в моем случае).

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(12-57-08).png)

*Вопросы:* 
Какова полоса пропускания этого интерфейса? - *BW 100000 Kbit*   
В каком состоянии находится VLAN 1 (77)? - *Vlan77 is up*  
В каком состоянии находится канальный протокол? - *line protocol is up*  

Шаг 2. Протестируем сквозное соединение, отправив эхо-запрос.

a.	C:\> ping 192.168.1.10 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(13-17-12).png)

b.	C:\> ping 192.168.1.2 (эхо-запрос на административный адрес интерфейса SVI коммутатора S1).

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(13-16-33).png)

Шаг 3. Проверим удаленное управление коммутатором S1.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/Screenshot_07.09.2022(13-56-27).png)

### 	Вопросы для повторения

1.	Зачем необходимо настраивать пароль VTY для коммутатора? *Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet (в нашем случае). VTY - виртуальный интерфейс, обеспечивающий удаленный доступ.*  
2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде? *Применить команду enable secret, которая обеспечивает бОльшую безопасность (по сравнению с enable password) - шифруя пароль.*
