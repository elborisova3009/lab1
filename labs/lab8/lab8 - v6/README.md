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
  Для примера коммутатор S2:  
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
