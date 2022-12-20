## Лабораторная работа. Настройка и проверка расширенных списков контроля доступа

### Топология  
![lab11](https://user-images.githubusercontent.com/112883654/208079808-5d973006-27da-4a07-81a3-7c71530fb5c6.png)  
### Таблица адресации  
![lab11](https://user-images.githubusercontent.com/112883654/208080096-011d2d05-a73e-438a-82fb-e2559138e4ea.png)  
### Таблица VLAN  
![lab11](https://user-images.githubusercontent.com/112883654/208080441-466b59a3-0fea-4460-ae58-6a7b43925ed5.png)  
### Задачи  
<details><summary> Раздел 1. Создание сети и настройка основных параметров устройства. </summary>  
 
 ### Часть 1.  
 Шаг 1. В CPT создам сеть согласно топологии.  
 
 ![image](https://user-images.githubusercontent.com/112883654/208670970-ccffc2c8-0ca3-48c9-b652-db22da4ec245.png)

 Шаг 2. Произведу базовую настройку маршрутизаторов по стандартному алгоритму, после чего дам вывод команды `show run` для каждого маршрутизатора.   
a.	Назначу маршрутизатору имя устройства.  
b.	Отключу поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначу class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначу cisco в качестве пароля консоли и включу вход в систему по паролю.  
e.	Назначу cisco в качестве пароля VTY и включу вход в систему по паролю.  
f.	Зашифрую открытые пароли.  
g.	Создам баннер с предупреждением о запрете несанкционированного доступа к устройству.  
h.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.    
 R1:  
![image](https://user-images.githubusercontent.com/112883654/208089986-8a5c6978-9b8e-458e-92e9-9d50b2a424cb.png)  
![image](https://user-images.githubusercontent.com/112883654/208090011-5796f3ae-9e01-48b9-8f58-599be18b19aa.png)  
![image](https://user-images.githubusercontent.com/112883654/208090097-ba4e23b8-107d-4ea1-a091-03573a084da2.png)  
 R2:  
![image](https://user-images.githubusercontent.com/112883654/208091005-4418a724-28d3-451f-b9c0-3232bb810ea9.png)  
![image](https://user-images.githubusercontent.com/112883654/208091060-316466fe-cf47-4508-88de-f678c50359db.png)  
![image](https://user-images.githubusercontent.com/112883654/208091117-438fb826-62fa-4314-81b6-c62f86694dc9.png)  
 
 Шаг 3. Произведу базовую настройку коммутаторов по стандартному алгоритму, после чего дам вывод команды `show run` для каждого коммутатора.   
a.	Присвою коммутатору имя устройства.  
b.	Отключу поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.  
c.	Назначу class в качестве зашифрованного пароля привилегированного режима EXEC.  
d.	Назначу cisco в качестве пароля консоли и включу вход в систему по паролю.  
e.	Назначу cisco в качестве пароля VTY и включу вход в систему по паролю.  
f.	Зашифрую открытые пароли.  
g.	Создам баннер с предупреждением о запрете несанкционированного доступа к устройству.  
h.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
 S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208092168-a90092fa-ab4d-4d80-a120-d6f4e7997835.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208092229-25e0fdbf-9997-4084-a84a-fb2318e63037.png)  
 S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208092678-dc9217c1-c1b7-4c11-b6f5-89c64ad424da.png)  
![image](https://user-images.githubusercontent.com/112883654/208092739-75e86dc3-c58c-4c68-9a7f-23a8f2142ace.png)  

  ### Часть 2. Настройка сетей VLAN на коммутаторах.  
Шаг 1. Создам сети VLAN на коммутаторах.  
a.	Создам VLAN по заданию, назову их в соответствии с таблицей VLAN.    
 S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208094534-d9d192af-60df-4751-9221-911ee44258c2.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208094574-fff4bbed-4529-471b-b1a1-55674d3765ac.png)  
S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208095107-c2280b7f-fbde-4088-b79c-00ff4c372aa7.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208095228-b6c24d28-d88b-4f79-9dc4-13ff62c1f25e.png)  
 b.	Настрою интерфейс управления и шлюз по умолчанию на каждом коммутаторе в соответствии с таблицей адресации.    
  S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208095566-8722ec69-5062-42fd-aff0-161bb4de8252.png)  
 S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208095796-e150f3c8-57e7-4499-98f3-8a74eb7c354d.png)  
c.	Назначу все неиспользуемые порты коммутатора VLAN Parking Lot, настрою их для статического режима доступа и административно деактивирую их (`interface range`).  
  S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208098229-03d6a754-9b12-4c48-8796-3e067dce81b6.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208098761-d2e158fa-6926-486c-894f-23443551e590.png)  
  S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208098807-fa723caf-74a3-446a-845c-a259fd8490ea.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208098848-287202f6-1bac-4e1e-a70b-6139ce0d9511.png)  
 
Шаг 2. Назначу сети VLAN соответствующим интерфейсам коммутаторов.  
a.	Назначу используемые порты соответствующей VLAN в соответствии с таблицей VLAN и настрою их для режима статического доступа.    
b.	Выполню команду `show vlan brief`, чтобы убедиться, что сети VLAN назначены правильным интерфейсам.  
  S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208658555-048b6652-cdc2-464d-90c9-0e4bdf40503e.png)  
  S2:   
![image](https://user-images.githubusercontent.com/112883654/208658979-b21a3c4e-7c62-4777-a13d-0e21b95440d4.png)  

 ### Часть 3. Настрою транки (магистральные каналы).  
Шаг 1. Вручную настрою магистральный интерфейс F0/1.  
 a.	Изменю режим порта коммутатора на интерфейсе F0/1, чтобы принудительно создать магистральную связь. Не забуду сделать это на обоих коммутаторах.  
 b.	В рамках конфигурации транка установлю для native vlan значение 1000 на обоих коммутаторах. При настройке двух интерфейсов для разных собственных VLAN сообщения об ошибках могут отображаться временно.  
 c.	В качестве другой части конфигурации транка укажу, что VLAN 10, 20, 30 и 1000 разрешены в транке.  
 S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208661958-e2e93509-79c3-45c8-a661-dfe2d8dc7441.png)  
 S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208662069-50d20513-4c63-4620-80fb-aadc59e713d6.png)  
 d.	Выполню команду `show interfaces trunk` для проверки портов магистрали, собственной VLAN и разрешенных VLAN через магистраль.    
  S1:  
 ![image](https://user-images.githubusercontent.com/112883654/208662369-efe88198-2bee-4e95-825f-de04038d2f9d.png)  
  S2:  
 ![image](https://user-images.githubusercontent.com/112883654/208662321-68835d5e-c069-4fd0-a2aa-888e7d761c3a.png)  
 
Шаг 2. Вручную настрою магистральный интерфейс F0/5 на коммутаторе S1.  
a.	Настрою интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.  
 ![image](https://user-images.githubusercontent.com/112883654/208663130-8b877645-05e8-486b-95ad-a642c8dd0894.png)
b.	Сохраню текущую конфигурацию в файл загрузочной конфигурации.  
 ![image](https://user-images.githubusercontent.com/112883654/208663164-f512b14a-0883-4fcc-a53a-33bc895a6327.png)  
c.	Использую команду `show run` для проверки настроек транка.  
 ![image](https://user-images.githubusercontent.com/112883654/208664346-162da512-fcb7-488e-9323-720d3dbda460.png)

 ### Часть 4. Настрою маршрутизацию.  
Шаг 1. Настройка маршрутизации между сетями VLAN на R1.  
a.	Активирую интерфейс G0/0/1 на маршрутизаторе.  
b.	Настрою подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Проверю, что подинтерфейс для собственной VLAN не имеет назначенного IP-адреса. Включу описание для каждого подинтерфейса.  
  ![image](https://user-images.githubusercontent.com/112883654/208665672-e1894d23-71a3-4223-a23f-cb0000451727.png)  
c.	Настрою интерфейс Loopback 1 на R1 с адресацией из приведенной выше таблицы.  
 ![image](https://user-images.githubusercontent.com/112883654/208665903-55005e2e-1301-4589-9e25-e64191b88b6a.png)  
d.	С помощью команды `show ip interface brief` проверю конфигурацию подынтерфейса.  
 ![image](https://user-images.githubusercontent.com/112883654/208665977-44c45af8-c395-478c-8d51-8af775c4ac60.png)  
 
Шаг 2. Настройка интерфейса R2 g0/0/1 с использованием адреса из таблицы и маршрута по умолчанию с адресом следующего перехода 10.20.0.1  
![image](https://user-images.githubusercontent.com/112883654/208666346-a1e36d12-ac10-453a-bc75-a7ca4547f1f6.png)  
 
### Часть 5. Настройка удаленого доступа. 
Шаг 1. Настрою все сетевые устройства для базовой поддержки SSH.   
a.	Создам локального пользователя с именем пользователя SSHadmin и зашифрованным паролем $cisco123!  
b.	Использую ccna-lab.com в качестве доменного имени.  
c.	Сгенерирую криптоключи с помощью 1024 битного модуля.  
d.	Настрою первые пять линий VTY на каждом устройстве, чтобы поддерживать только SSH-соединения и с локальной аутентификацией.  
 ![image](https://user-images.githubusercontent.com/112883654/208666827-a86aa4e5-ee7e-45f7-b1c0-22540307e142.png)  

Шаг 2. Включу защищенные веб-службы с проверкой подлинности на R1.  
a.	Включу сервер HTTPS на R1 `ip http secure-server`.   
b.	Настрою R1 для проверки подлинности пользователей, пытающихся подключиться к веб-серверу `ip http authentication local`.  
 *Ограничения CPT*  
 ![image](https://user-images.githubusercontent.com/112883654/208667232-2e3b22f5-a8e9-47bd-a375-701d52263ee2.png)  
 
 ### Часть 6. Проверка подключения.  
Шаг 1. Настрою узлы ПК согласно таблице адресации.  
 ![image](https://user-images.githubusercontent.com/112883654/208671830-b9021fa0-c840-4a5c-aebc-bfe5d5099021.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208671697-fd84d020-29ed-4f97-95a0-dbbb5878512a.png)  
Шаг 2. Выполню следующие тесты:  
 ![image](https://user-images.githubusercontent.com/112883654/208667443-d626c6b3-de92-4602-9655-1c4cb278a97e.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208672563-ce552fb6-b28e-4afd-b651-f0b4a9cc280a.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208673482-242cc7da-377f-45cc-8551-b425ed1f4f6b.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208675101-6252ae9a-3f93-49ea-b6bd-63da76dd870a.png)  
 ![image](https://user-images.githubusercontent.com/112883654/208674902-1ae331ca-3d3d-4a53-a78d-c9faceb63e65.png) 

</details> 



<details><summary> Раздел 2. Настройка и проверка списков расширенного контроля доступа. </summary>  
