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
  a.	Выполню команду `ipconfig /all` на PC-A и посмотрю на результат. *В рамках менторской встречи конфиг был скорректирован, актуального скриншота нет.*      
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
*В рамках менторской встречи выяснилось, что на интерфейсе G0/0/1 маршрутизатора R1 у меня был ошибочно установлен флаг MANAGED. Отменю через no-команду в режиме глобальной конфигурации: `no ipv6 nd managed-config-flag`.*
Проверю, что настройка стала корректной:  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2025-11-2022%20172012.jpg)  
  
  c.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
  d.	Перезапущу PC-A.  
  e.	Проверю вывод `ipconfig /all` и обращу внимание на изменения.  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2025-11-2022%20171918.jpg)  
  f.	Пинг IP-адреса интерфейса G0/1 R2 - потеря пакетов.  
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2024-11-2022%20173553.jpg)  
  *Работа над ошибками.  
На R1 обнаружен лишний неверный маршрут, который требует отмены через no-команду в режиме глобальной конфигурации.  
Оставлю только необходимый: `ipv6 route ::/0 2001:DB8:ACAD:2::2`.  
Кроме того, при проверке всех настроенных маршрутов, на R2 тоже обнаружен лишний неверный маршрут. Аналогично отменю неверный через no-команду в режиме глобальной конфигурации.  
Оставлю только необходимый: `ipv6 route ::/0 2001:db8:acad:2::1`.*    
  Теперь пинг IP-адреса интерфейса G0/1 R2 успешен.  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2030-11-2022%20134020.jpg)  
  </details> 
  
  <details><summary> Часть 4. Настройка и проверка состояния DHCPv6 сервера на R2. </summary>   
  
  *Задание изменено по согласованию с ментором.*  
  
  В части 4 настрою R2 для ответа на запросы DHCPv6 от локальной сети на R2.  
  a.	Создам пул DHCPv6 на R2 для сети 2001:db8:acad:3:aaa::/80. Это предоставит адреса локальной сети, подключенной к интерфейсу G0/0/1 на R2 (интерфейс, который смотрит на компьютер - то есть в сеть, где будет работать dhcp).  
  В составе пула задам DNS-сервер 2001:db8:acad: :254 и задам доменное имя STATEFUL.com.  
  
  ```  
R2(config)# ipv6 dhcp pool R2-STATEFUL
R2(config-dhcp)# address prefix 2001:db8:acad:3:aaa::/80
R2(config-dhcp)# dns-server 2001:db8:acad::254
R2(config-dhcp)# domain-name STATEFUL.com
```  
b.	Назначу только что созданный пул DHCPv6 интерфейсу g0/0/1 на R2.
```  
R2(config)# interface g0/0/1
R2(config-if)# ipv6 dhcp server R2-STATEFUL
```  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20132446.jpg)  
*По итогам работы над ошибками:*  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20132525.jpg)  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20132540.jpg) 
  </details> 
  
  <details><summary> Часть 5. Настройка и проверка DHCPv6 Relay на R2.</summary>  
  В части 5 по заданию было необходимо настроить и проверить ретрансляцию DHCPv6 на R2, позволяя PC-B получать адрес IPv6.  
  
а. *Так как в CPT не реализована возможность настройки проброса и R2 технически не может быть задан в качестве агента DHCP-ретрансляции для локальной сети на G0/0/1, эта часть будет опущена.  
b. Выше я вручную настроила маршрутизатор R2 на предоставление адреса PCB. Проверю:*  
  
![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20133420.jpg)  *Обращу внимание на вывод, что используется префикс 2001:db8:acad:3::*  \
 c. * Затем на PC-B проверю адрес SLAAC, который он генерирует командой `ipconfig /all`:*   
 ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20133632.jpg)  
  d.	Проверю связность с помощью пинга от PCB до IP-адреса интерфейса R1 G0/0/1.  
  ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20134758.jpg)  
  e.	Проверю связность с помощью пинга от PCA до IP-адреса интерфейса R1 G0/0/1.  
   ![lab8](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/lab8%20-%20v6/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2005-12-2022%20134810.jpg)  
  
  
  

