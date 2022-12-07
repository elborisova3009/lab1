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
Шаг 1. Релизация магистральных соединений 802.1Q.  

a.	Настрою все магистральные порты Fa0/1 на обоих коммутаторах для использования VLAN 333 в качестве native VLAN.  
  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151344.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151508.jpg)  
 
b.	Убедитесь, что режим транкинга успешно настроен на всех коммутаторах.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20151757.jpg)  
  
c.	Отключу согласование DTP F0/1 на S1 и S2.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20160642.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20160807.jpg) 
  
d.	Проверю с помощью команды  `show interfaces `:    
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20160657.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20160817.jpg)   
 
  Шаг 2. Настройка портов доступа.  
a.	На S1 настрою F0/5 и F0/6 в качестве портов доступа и свяжу их с VLAN 10.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20161823.jpg)  
  
b.	На S2 настрою порт доступа Fa0/18 и свяжу его с VLAN 10.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20161907.jpg)  
  
  Шаг 3. Безопасность неиспользуемых портов коммутатора.   
a.	На S1 и S2 перемещу неиспользуемые порты из VLAN 1 во VLAN 999 и отключу неиспользуемые порты.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20162445.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20162535.jpg)  
 
b.	Проверю, что неиспользуемые порты отключены и связаны с VLAN 999, применив команду `show interfaces status`.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20163003.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20163027.jpg)  
  
</details> 

<details><summary> Шаг 4. Документирование и реализация функций безопасности порта. </summary>  
Интерфейсы F0/6 на S1 и F0/18 на S2 настроены, как порты доступа.  

На этом шаге я также настрою безопасность портов на этих двух портах доступа.  
  
a.	На S1 введу команду `show port-security interface f0/6` для отображения настроек по умолчанию безопасности порта для интерфейса F0/6.  
Вывод команды:  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20163636.jpg)  
Запишу свои ответы в таблице ниже.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20163945.jpg)  
  
b.	На S1 включу защиту порта на F0/6 со следующими настройками:    
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20164608.jpg)  
CPT имеет ограничения функционала.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20164729.jpg)  
  
c.	Отображу примененные настройки безопасности порта для интерфейса F0/6.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20165337.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20170136.jpg)  
  
d.	На S2 включу защиту порта на F0/18.    
Настрою каждый активный порт доступа, чтобы он автоматически добавлял адреса МАС, изученные на этом порту, в текущую конфигурацию.  
e.	На S2 настрою следующие параметры безопасности порта F/18:  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20171543-1.jpg)  
f.	На S2 проверю функции безопасности порта F0/18.  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20171016.jpg)  
![lab9](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab9/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2006-12-2022%20171233.jpg)  
 
  *После применения на PCB команд `ipconfig /release` и `ipconfig /renew` картина следующая:  
  ![lab9](https://user-images.githubusercontent.com/112883654/206185786-b8940c7d-5492-4710-a1cf-e5d18eab1bd9.png)  
  В рамках менторской встречи выснилось, что на Шаге 2 в части a. не отработала команда `ip dhcp relay information trusted` (что есть результат ограниченного функционала CPT). Как следствие, не включилось "доверие" к опции 82 - проявилось в выводе команды `show ip dhcp snooping` на коммутаторе S2:    
![lab9](https://user-images.githubusercontent.com/112883654/206187382-a6537f86-eb12-48ab-85db-fd7ddba2e1c7.png)  
Требуется на коммутаторе S2 выключить данную опцию: 
![lab9](https://user-images.githubusercontent.com/112883654/206188472-cecc99c2-e033-4f87-a427-79c91148f67f.png)  
  В итоге на PCB успешно отработал DHCP:*  
![lab9](![image](https://user-images.githubusercontent.com/112883654/206188649-0cd81623-ddfa-41f9-ac23-41b0e04b3d6d.png)  
  
  


  
  

 




  
  
</details> 
  
<details><summary> Шаг 5. Реализовать безопасность DHCP snooping. </summary>  

На S2:  
a.  Включу DHCP snooping и настрою DHCP snooping во VLAN 10.  
b.	Настрою магистральные порты, как доверенные порты.  
c.	Ограничу ненадежный порт Fa0/18 пятью DHCP-пакетами в секунду.  
d.	Проверю DHCP Snooping.  
  
</details> 
