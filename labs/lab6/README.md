### Лабораторная работа 6. Внедрение маршрутизации между виртуальными локальными сетями 

### Топология
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20102253.jpg)

### Таблица адресации
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20102449.jpg)

### Таблица VLAN
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20102459-3.jpg)

### Задачи
Часть 1. Создание сети и настройка основных параметров устройства  
Часть 2. Создание сетей VLAN и назначение портов коммутатора  
Часть 3. Настройка транка 802.1Q между коммутаторами  
Часть 4. Настройка маршрутизации между сетями VLAN  
Часть 5. Проверка, что маршрутизация между VLAN работает  

### Часть 1. Создание сети и настройка основных параметров устройства

Шаг 1. В CPT cоздаю сеть согласно топологии.  

Шаг 2. Настрою базовые параметры для маршрутизатора R1:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20112704.jpg)

Show Run:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20112857.jpg)

Шаг 3. Настрою базовые параметры каждого коммутатора (на примере S1):

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20114144.jpg)

Show Run:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20114317.jpg)

Шаг 4. Настрою узлы ПК (согласно таблице адресации).

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20115717.jpg)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20115754.jpg)

### Часть 2. Создание сетей VLAN и назначение портов коммутатора

Шаг 1. Создам сети VLAN на коммутаторах.

a.	Создам и назову необходимые VLAN на каждом коммутаторе из таблицы выше. 

Vlan 10 для S1: 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20125154.jpg)

Vlan 20 для S1: 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20130607.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20130622.jpg)

И оставшиеся vlan для S1:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20132158.jpg)

Аналогично проведу работу для S2, проиллюстрирую выводом команды show vlan:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20133122.jpg)

b.	Настрою интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации. 

S1:  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20134412.jpg)

S2:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20155036.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20155048.jpg)

c.	Все неиспользуемые порты коммутаторов уже назначены во VLAN Parking_Lot, также они уже настроены для статического режима доступа.  
Теперь административно деактивирую их.

S1:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20160116.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20160153.jpg)

S2:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20160529.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2012-10-2022%20160644.jpg)














