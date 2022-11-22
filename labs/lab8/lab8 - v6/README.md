## Лабораторная работа - Настройка DHCP. Реализация DHCPv6 

### Топология

![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20132045.jpg)  

### Таблица адресации
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2017-11-2022%20110014.jpg)
  
###	Задачи

<details><summary> Часть 1. Создание сети и настройка основных параметров устройства. </summary> 

  Шаг 1.	Создам в CPT сеть согласно заданной топологии.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2001-11-2022%20175036.jpg)  
  Шаг 2. Настрою базовые параметры каждого коммутатора - необязательный шаг, поэтому по сокращенной программе:  
```
  S1:
enable
configure terminal
hostname S1
no ip domain lookup
exit
copy run start

show run
```
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
  Для примера коммутатор S1:  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20134726.jpg)  
  

  
  
  

a.	Присвойте коммутатору имя устройства.
b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
e.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
f.	Зашифруйте открытые пароли.
g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
h.	Отключите все неиспользуемые порты.
i.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
  
  
  

  
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
  
  <details><summary> Часть 2. Проверка назначения адреса SLAAC от R1.</summary> 

  </details> 
  
 <details><summary> Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1.</summary> 

  </details> 
  
  <details><summary> Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1.</summary> 

  </details> 
  
  <details><summary> Часть 5. Настройка и проверка DHCPv6 Relay на R2.</summary>

  </details>   
