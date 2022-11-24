## Лабораторная работа - Настройка DHCP. Реализация DHCPv6 

### Топология

![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20132045.jpg)  

### Таблица адресации
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2017-11-2022%20110014.jpg)
  
###	Задачи

<details><summary> Часть 1. Создание сети и настройка основных параметров устройства. </summary> 

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
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20170453.jpg)    
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20170527.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20170539.jpg)  
  
Шаг 3. Произведу базовую настройку маршрутизаторов.  
a.	Назначу маршрутизаторам имя устройства.  
b.	Отключу поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначу class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначу cisco в качестве пароля консоли и включу вход в систему по паролю.  
e.	Назначу cisco в качестве пароля VTY и включу вход в систему по паролю.  
f.	Зашифрую открытые пароли.  
g.	Создам баннер с предупреждением о запрете несанкционированного доступа к устройству.  
h.	Активирую IPv6-маршрутизацию.  
i.	Сохраню текущую конфигурацию в файл загрузочной конфигурации. 
  
   Для примера маршрутизатор R2:   
```  
  enable
configure terminal
hostname R2
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
ipv6 unicast-routing
exit
copy run start
show run
```    
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20165830.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20165912.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2022-11-2022%20165930.jpg)  
Шаг 4. Настройка интерфейсов и маршрутизации для обоих маршрутизаторов.  
a.	Настрою интерфейсы G0/0/0 и G0/1 на R1 и R2 с адресами IPv6, указанными в таблице выше.  
b.	Настрою маршрут по умолчанию на каждом маршрутизаторе, который указывает на IP-адрес G0/0/0 на другом маршрутизаторе.  
c.	Проверю работу маршрутизации с помощью пинга адреса G0/0/1 R2 из R1.  
d.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
  
Маршрутизатор R1:   
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20163116.jpg)  
Маршрутизатор R2:  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20163523.jpg)  </details> 
  
  <details><summary> Часть 2. Проверка назначения адреса SLAAC от R1.</summary>  
  
Проверю, получает ли узел PC-A адрес IPv6 с помощью метода SLAAC.  
Настрою сетевой адаптер PC-A на автоматическую настройки IPv6.  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20164701.jpg)  
Командой ipconfig проверю, присвоил ли PC-A себе адрес из сети 2001:db8:1::/64.  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20164837.jpg)  
  Вопрос: Откуда взялась часть адреса с идентификатором хоста?  
  *Адрес EUI-64 получается на основе MAC-адреса интерфейса /  64-битный адрес генерируется случайно*

</details> 
  
 <details><summary> Часть 3. Настройка и проверка сервера DHCPv6 без гражданства на R1.</summary>  
В части 3 производится настройка и проверка состояния DHCP-сервера на R1. Цель состоит в том, чтобы предоставить PC-A информацию о DNS-сервере и домене.  
  
  Шаг 1. Более подробно изучу конфигурацию PC-A.  
  a.	Выполню команду `ipconfig /all` на PC-A и посмотрю на результат. 
  Из задания:  
  ```  
   Host Name . . . . . . . . . . . . : НАСТОЛЬНАЯ 3FR7RKA
   Primary Dns Suffix . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix . : 
   Description . . . . . . . . . . . : Intel(R) 852574L Gigabit Network Connection 
   Physical Address. . . . . . . . . : 00-50-56-83-63-6D
   IPv6 Address. . . . . . . . . . . : 2001:db8:acad:1:5c43:ee7c:2959:da68(Preferred)
   Temporary IPv6 Address. . . . . . : 2001:db8:acad:1:3c64:e4f9:46e1:1f23(Preferred)
   Link-local IPv6-адрес. . . . . : fe80::5c43:ee7c:2959:da68%6(Preferred)
   IPv4 Address. . . . . . . . . . . : 169.254.218.104(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Шлюз по умолчанию . . . . . . . . .: fe80።1%6
   DHCPv6 IAID . . . . . . . . . . . : 50334761
   DHCPv6 Client DUID.  . . . . . . . : 00-01-00-01-24-F5-CE-A2-00-50-56-B3-63-6D
   DNS-серверы . . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBIOS over Tcpip. . . . . . . . : Enabled
   ```  
   Из CRT (эмулируется криво или закралась ошибка???)  
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20170059.jpg)  
b.	Я должна была увидеть, что основной DNS-суффикс отсутствует. И что предоставленные адреса DNS-сервера являются адресами «локального сайта anycast», а не одноадресными адресамим, как ожидалось.  
  
Шаг 2. Настрою R1 для предоставления DHCPv6 без состояния для PC-A.  
a.	Создам пул DHCP IPv6 на R1 с именем R1-STATELESS. В составе этого пула назначу адрес DNS-сервера как 2001:db8:acad: :1, а имя домена — stateless.com.  
```  
R1(config)# ipv6 dhcp pool R1-STATELESS
R1(config-dhcp)# dns-server 2001:db8:acad::254
R1(config-dhcp)# domain-name STATELESS.com
```  
b.	Настрою интерфейс G0/0/1 на R1, чтобы предоставить флаг конфигурации OTHER для локальной сети R1 и укажу только что созданный пул DHCP в качестве ресурса DHCP для этого интерфейса.  
``` 
R1(config)# interface g0/0/1
R1(config-if)# ipv6 nd other-config-flag 
R1(config-if)# ipv6 dhcp server R1-STATELESS
```   
c.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
  
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20172135.jpg)  
  d.	Перезапущу PC-A.  
  e.	Проверю вывод `ipconfig /all` и обращу внимание на изменения.  
Из задания:  
  ```
   Host Name . . . . . . . . . . . . : DESKTOP-3FR7RKA
   Primary Dns Suffix . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : STATELESS.com

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix . : STATELESS.com
   Описание . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-50-56-83-63-6D
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : 2001:db8:acad:1:5c43:ee7c:2959:da68(Preferred)
   Temporary IPv6 Address. . . . . . : 2001:db8:acad:1:3c64:e4f9:46e1:1f23(Preferred)
   Link-local IPv6-адрес. . . . . : fe80::5c43:ee7c:2959:da68%6(Preferred)
   IPv4 Address. . . . . . . . . . . : 169.254.218.104(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . .: fe80።1%6
   DHCPv6 IAID . . . . . . . . . . . : 50334761
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-24-F5-CE-A2-00-50-56-B3-63-6D
   DNS Servers . . . . . . . . . . . : 2001:db8:acad። 254
   NetBIOS over Tcpip. . . . . . . . : Enabled
   Список поиска DNS-суффиксов подключения: 
                                       STATELESS.com
 ```  
  Из CRT:   
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20172606.jpg)  
  f.	Пинг IP-адреса интерфейса G0/1 R2 - есть потеря пакетов.  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20173553.jpg)  
  
  </details> 
  
  <details><summary> Часть 4. Настройка и проверка состояния DHCPv6 сервера на R1.</summary> 
  
  В части 4 настраивается R1 для ответа на запросы DHCPv6 от локальной сети на R2.  
a.	Создам пул DHCPv6 на R1 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2. В составе пула задам DNS-сервер 2001:db8:acad: :254 и задам доменное имя STATEFUL.com.  
 ```  
R1(config)# ipv6 dhcp pool R2-STATEFUL
R1(config-dhcp)# address prefix 2001:db8:acad:3:aaa::/80
R1(config-dhcp)# dns-server 2001:db8:acad::254
R1(config-dhcp)# domain-name STATEFUL.com
b.	Назначьте только что созданный пул DHCPv6 интерфейсу g0/0/0 на R1.
R1(config)# interface g0/0/0
R1(config-if)# ipv6 dhcp server R2-STATEFUL
   ```  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20173955.jpg)  

  </details> 
  
  <details><summary> Часть 5. Настройка и проверка DHCPv6 Relay на R2.</summary>  
В части 5 необходимо настроить и проверить ретрансляцию DHCPv6 на R2, позволяя PC-B получать адрес IPv6.  

  Шаг 1. Включу PC-B и проверю адрес SLAAC, который он генерирует командой `ipconfig /all`.    
Из задания:  
 ```  
   Host Name . . . . . . . . . . . . : DESKTOP-3FR7RKA
   Primary Dns Suffix . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix . : 
   Description . . . . . . . . . . . : Intel(R) 82574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-50-56-B3-7B-06
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : 2001:db8:acad:3:a0f3:3d39:f9fb:a020(Preferred) 
   Temporary IPv6 Address. . . . . . : 2001:db8:acad:3:d4f3:7b16:eeee:b2b5(Preferred) 
   Link-local IPv6 address. . . . . : fe80::a0f3:3d39:f9fb:a020%6(Preferred) 
   IPv4 Address. . . . . . . . . . . : 169.254.160.32(Preferred) 
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . .: fe80።1%6
   DHCPv6 IAID . . . . . . . . . . . : 50334761
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-24-F2-08-38-00-50-56-B3-7B-06
   DNS Servers . . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBIOS over Tcpip. . . . . . . . : Enabled
   ```  
  
  Из CRT - ???:    
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20175202.jpg)  
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20175126.jpg)  
  
Обращу внимание на вывод, что используется префикс 2001:db8:acad:3:: - ???  
  
Шаг 2. Настрою R2 в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1.  
a.	Настрою команду `ipv6 dhcp relay` на интерфейсе R2 G0/0/1, указав адрес назначения интерфейса G0/0/0 на R1. Также настрою команду `managed-config-flag`.  
    ```  
interface g0/0/1
ipv6 nd managed-config-flag
ipv6 dhcp relay destination 2001:db8:acad:2::1 g0/0/0 
   ``` 
CRT - ???  
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20180128.jpg)  
 b.	Сохраните конфигурацию `copy run start`.
Закрою окно настройки.  
  
Шаг 3. Попытка получить адрес IPv6 из DHCPv6 на PC-B.  
a.	Перезапущу PC-B.
b.	Открою командную строку на PC-B и выполню команду `ipconfig /all` и проверью выходные данные, чтобы увидеть результаты операции ретрансляции DHCPv6.
Из задания:  
  ``` 
   Host Name . . . . . . . . . . . . : DESKTOP-3FR7RKA
   Primary Dns Suffix . . . . . . . : 
   Node Type . . . . . . . . . . . . : Hybrid
   IP Routing Enabled. . . . . . . . : No
   WINS Proxy Enabled. . . . . . . . : No
   DNS Suffix Search List. . . . . . : STATEFUL.com

Ethernet adapter Ethernet0:

   Connection-specific DNS Suffix . : STATEFUL.com
   Description . . . . . . . . . . . : Intel(R) 852574L Gigabit Network Connection
   Physical Address. . . . . . . . . : 00-50-56-B3-7B-06
   DHCP Enabled. . . . . . . . . . . : Yes
   Autoconfiguration Enabled . . . . : Yes
   IPv6 Address. . . . . . . . . . . : 2001:db8:acad3:aaaa:7104:8b7d:5402(Preferred)
   Lease Obtained. . . . . . . . . . : Sunday, October 6, 2019 3:27:13 PM
   Lease Expires . . . . . . . . . . Tuesday, October 8, 2019 3:27:13 PM
   Link-local IPv6-адрес. . . . . : fe80::a0f3:3d39:f9fb:a020%6(Preferred)
   IPv4 Address. . . . . . . . . . . : 169.254.160.32(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . .: fe80። 2% 6
   DHCPv6 IAID . . . . . . . . . . . : 50334761
   DHCPv6 Client DUID. . . . . . . . : 00-01-00-01-24-F2-08-38-00-50-56-B3-7B-06
   DNS Servers . . . . . . . . . . . : 2001:db8:acad። 254
   NetBIOS over Tcpip. . . . . . . . : Включен
   Список поиска DNS-суффиксов подключения: STATEFUL.com  
    ```   
  
  Из CRT - ???:  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20181020.jpg)  
c.	Проверю подключение с помощью пинга IP-адреса интерфейса R1 G0/0/1.  
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20180128.jpg)  
  </details>   
