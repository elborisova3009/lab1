## Лабораторная работа - Конфигурация безопасности коммутатора

### Топология

![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20145310.jpg)

### Таблица адресации
  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20150117.jpg)  
  
###	Задачи

<details><summary> Часть 1. Настройка основного сетевого устройства. </summary>  
  
  Шаг 1. Создам в CPT сеть согласно топологии. 
    
 ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20153919-1.jpg)  
  
  Шаг 2. Настрою маршрутизатор R1.  
a.	Загружу следующий конфигурационный скрипт на R1:  
  
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20164858.jpg)  
    
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20155823.jpg)    
    
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20155835.jpg)  
   
b.	Проверю текущую конфигурацию на R1, используя команду `show ip interface brief`  
c.	Отконтролирую, что IP-адресация применена, а соответствующие интерфейсы находятся в состоянии up / up.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20160222.jpg)  
    
   Шаг 3. Настройка и проверка основных параметров коммутатора.    
a.	Настрою имена хостов для коммутаторов S1 и S2.  
 ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20165957.jpg)  
 ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20170025.jpg)  
b.	Запрещу нежелательный поиск в DNS.  
c.	Настрою описания интерфейсов для портов, которые используются в S1 и S2.  
d.	Установлю для шлюза по умолчанию (для VLAN управления) значение 192.168.10.1 на обоих коммутаторах.  
     S1:  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20172940.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20173005.jpg)  
     S2:  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20173156.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20173128.jpg)  

 </details> 
  
  <details><summary> Часть 2. Настройка сетей VLAN.</summary>  
  
a. Сконфигрурирую (добавлю) VLAN 10 на S1 и S2 и назову его Management.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20143733.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20143835.jpg)  
  
b. Сконфигурирую SVI для VLAN 10.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20144911.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20145006.jpg)  
  
c. На двух коммутатолрах настрою: VLAN 333 с именем Native, VLAN 999 с именем ParkingLot.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20145155.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20145304.jpg)  
  
</details> 

 <details><summary> Часть 3. Настройки безопасности коммутатора.</summary>  
a.	Настрою все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.  
  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151344.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151508.jpg)  
 
b.	Убедитесь, что режим транкинга успешно настроен на всех коммутаторах.  
 ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151757.jpg

 

</details> 


  Шаг 1.	Создам в CPT сеть согласно заданной топологии.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20175036.jpg)  
  Шаг 2. Настрою базовые параметры каждого коммутатора - необязательный шаг, поэтому по сокращенной программе.  
  Для примера коммутатор S2:  
   ```
S2: 
enable
configure terminal
hostname S2
no ip domain lookup
exit
copy run start

show run
```
