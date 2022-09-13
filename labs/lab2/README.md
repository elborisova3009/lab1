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
 
 Шаг 1. Запишем МАС-адреса сетевых устройств.
 
 a.	Откроем командную строку на PC-A и PC-B и введем команду ipconfig /all  
 
 ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-32-27).png)
 ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-33-22).png)
 
  Физические адреса адаптера Ethernet:  
  PC-A: Physical Address................: 0030.F2E3.DD44  
  PC-B: Physical Address................: 000B.BEE9.18AC
  
  MAC-адрес компьютера PC-A: 0030.F2E3.DD44  
  MAC-адрес компьютера PC-B: 000B.BEE9.18AC  
  
  b.	Подключимся к коммутаторам S1 и S2 и введем команду show interface F0/1 на каждом коммутаторе
  
  ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-58-41).png)
  ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(15-58-04).png)
  
  Адреса оборудования во второй строке выходных данных команды (или зашитый адрес — bia):
  
  МАС-адрес коммутатора S1 Fast Ethernet 0/1: address is 000c.cfa0.5401 (bia 000c.cfa0.5401)  
  МАС-адрес коммутатора S2 Fast Ethernet 0/1: address is 0000.0cc8.7001 (bia 0000.0cc8.7001)
  
  
  Шаг 2. Просмотрим таблицу МАС-адресов коммутатора.
  S2# show mac address-table
  
  ![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(17-27-11).png)
  
1. Записаны ли в таблице МАС-адресов какие-либо МАС-адреса? *Да.*    
2. Какие МАС-адреса записаны в таблице? С какими портами коммутатора они сопоставлены и каким устройствам принадлежат? Игнорируйте МАС-адреса, сопоставленные с центральным процессором.   
*000c.cfa0.5401 Fa0/1 VLAN 1 коммутатора S1*  
3. Если вы не записали МАС-адреса сетевых устройств в шаге 1, как можно определить, каким устройствам принадлежат МАС-адреса, используя только выходные данные команды show mac address-table? Работает ли это решение в любой ситуации?   
*Столбец Ports показывает интерфейс с данным адресом.*  
```Не уверена в правильности ответа. Прошу поправить.```

  Шаг 3. Очистим таблицу МАС-адресов коммутатора S2 и снова отобразим таблицу МАС-адресов.
  
a.	S2# clear mac address-table dynamic
b.	Снова быстро введем команду show mac address-table.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(17-42-30).png)

Указаны ли в таблице МАС-адресов адреса для VLAN 1? Указаны ли другие МАС-адреса? *Нет.*  
Через 10 секунд введем команду show mac address-table и нажмем клавишу ввода. Появились ли в таблице МАС-адресов новые адреса?  
*Да, который и был: 000c.cfa0.5401 Fa0/1 VLAN 1 коммутатора S1.*   

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(17-44-17).png)

с.	```Факультативно - вопросительно.```   
После эхо-запроса от коммутатора S2 к PC-A в таблице МАС-адресов появляется МАС-адрес: 0000.0cc8.7001 Fa0/1 VLAN 1 коммутатора S2.   
Теперь таблица выглядит так.  
```Нормально ли это?``` 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_12.09.2022(17-44-37).png)

Шаг 4. С компьютера PC-B отправляем эхо-запросы устройствам в сети и просмотрим таблицу МАС-адресов коммутатора.

a.	На компьютере PC-B откроем командную строку и *еще раз* введем команду arp-a.  
```Почему "еще раз"?```

Не считая адресов многоадресной и широковещательной рассылки, сколько пар IP- и МАС-адресов устройств было получено через протокол ARP?  
*3 пары адресов: PC-A, S1, S2*  
```Разве не должно быть 2 пары?..```  
```Не вижу адресов многоадресной и широковещательной рассылки, почему?```  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_13.09.2022(14-19-23).png)

b.	Из командной строки PC-B отправляем эхо-запросы на компьютер PC-A, а также коммутаторы S1 и S2.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_13.09.2022(14-56-22).png)

От всех ли устройств получены ответы? *От всех.*

c.	Подключаемся через консоль к коммутатору S2, вводим команду show mac address-table.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_13.09.2022(15-04-57).png)

Добавил ли коммутатор в таблицу МАС-адресов дополнительные МАС-адреса? Если да, то какие адреса и устройства?  
*МАС-адреса компьютеров PC-A, PC-B и интерфейсов Fa0/1 and Vlan1 коммутатора S1.*  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_13.09.2022(15-04-57).png)

На компьютере PC-B откройте командную строку и еще раз введите команду arp -a.
Появились ли в ARP-кэше компьютера PC-B дополнительные записи для всех сетевых устройств, которым были отправлены эхо-запросы?  
```Нет,  вижу те же записи для PC-A, S1, S2, что и в пункте a. Шага 3. Части 2.```    
```Нормально ли это?```    
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab2/Screenshot_13.09.2022(15-25-15).png)

### Вопросы для повторения
  
В сетях Ethernet данные передаются на устройства по соответствующим МАС-адресам. Для этого коммутаторы и компьютеры динамически создают ARP-кэш и таблицы МАС-адресов. Если компьютеров в сети немного, эта процедура выглядит достаточно простой. Какие сложности могут возникнуть в крупных сетях?  
*В крупных сетях большое количество запросов замедляет работу всей сети.*




















