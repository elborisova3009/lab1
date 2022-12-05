## Лабораторная работа - Конфигурация безопасности коммутатора

### Топология

![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20145310.jpg)

### Таблица адресации
  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20150117.jpg)  
  
###	Задачи

<details><summary> Часть 1. Настройка основного сетевого устройства. </summary>  
  <details><summary> Шаг 1. Создам в CPT сеть согласно топологии. </summary>    
    
 ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20153919-1.jpg)  
  <details><summary> Шаг 2. Настрою маршрутизатор R1. </summary>  
a.	Загружу следующий конфигурационный скрипт на R1:  
    
```
enable
configure terminal
hostname R1
no ip domain lookup
ip dhcp excluded-address 192.168.10.1 192.168.10.9
ip dhcp excluded-address 192.168.10.201 192.168.10.202
!
ip dhcp pool Students
 network 192.168.10.0 255.255.255.0
 default-router 192.168.10.1
 domain-name CCNA2.Lab-11.6.1
!
interface Loopback0
 ip address 10.10.1.1 255.255.255.0
!
interface GigabitEthernet0/0/1
 description Link to S1
 ip dhcp relay information trusted
 ip address 192.168.10.1 255.255.255.0
 no shutdown
!
line con 0
 logging synchronous
 exec-timeout 0 0
```  
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20164858.jpg)  
    
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20155823.jpg)    
    
   ![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20155835.jpg)  
   
b.	Проверю текущую конфигурацию на R1, используя команду `show ip interface brief`  
c.	Отконтролирую, что IP-адресация применена, а соответствующие интерфейсы находятся в состоянии up / up.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20160222.jpg)  

  </details> 
  
   <details><summary> Шаг 3. Настройка и проверка основных параметров коммутатора. </summary>  
     
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
    
 </details> 
  
  <details><summary> Часть 2. Настройка сетей VLAN.</summary>  
  
•	Сконфигруриуйте VLAN 10.
•	Сконфигруриуйте SVI для VLAN 10.
•	Настройте VLAN 333 с именем Native на S1 и S2.
•	Настройте VLAN 999 с именем ParkingLot на S1 и S2.
</details> 

 <details><summary> Часть 3. Настройки безопасности коммутатора.</summary>  
 
•	Реализация магистральных соединений 802.1Q.
•	Настройка портов доступа
•	Безопасность неиспользуемых портов коммутатора
•	Документирование и реализация функций безопасности порта.
•	Реализовать безопасность DHCP snooping .
•	Реализация PortFast и BPDU Guard
•	Проверка сквозной связанности.

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
