### Лабораторная работа 7. Развертывание коммутируемой сети с резервными каналами

#### Топология 
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20114403.jpg)

#### Таблица адресации
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20114706-1.jpg)

#### Цели
Часть 1. Создание сети и настройка основных параметров устройства  
Часть 2. Выбор корневого моста  
Часть 3. Наблюдение за процессом выбора протоколом STP порта, исходя из стоимости портов  
Часть 4. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов  

#### Часть 1:	Создание сети и настройка основных параметров устройства

Шаг 1:	Создайте сеть согласно топологии.







Шаг 2:	Выполнение инициализации и перезагрузки коммутаторов в CPT не требуется.

Шаг 3:	Настрою базовые параметры каждого коммутатора. Для примера S1:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20125135.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20125932.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20125951.jpg)

S1 show run:  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20130211.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20130227.jpg)

Аналогично для S2 и S3.  
S2 show run:   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20131627.jpg)  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20131639.jpg)  
S3 show run:      
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20141520.jpg)   
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20141532.jpg)

Шаг 4:	Проверю связь.  
Нет пингов.

Дополню конфиги настройкой магистральных портов, задам VLAN 88 - native.  

Успешно ли выполняется эхо-запрос от коммутатора S1 на коммутатор S2? *Да.*  

Успешно ли выполняется эхо-запрос от коммутатора S1 на коммутатор S3? *Да.*  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20144526.jpg)  


Успешно ли выполняется эхо-запрос от коммутатора S2 на коммутатор S3?	*Да.*    
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20145150.jpg)  

#### Часть 2:	Определение корневого моста  
Для каждого экземпляра протокола spanning-tree (коммутируемая сеть LAN или широковещательный домен) существует коммутатор, выделенный в качестве корневого моста. Корневой мост служит точкой привязки для всех расчётов протокола spanning-tree, позволяя определить избыточные пути, которые следует заблокировать.  
Процесс выбора определяет, какой из коммутаторов станет корневым мостом. Коммутатор с наименьшим значением идентификатора моста (BID) становится корневым мостом. Идентификатор BID состоит из значения приоритета моста, расширенного идентификатора системы и MAC-адреса коммутатора. Значение приоритета может находиться в диапазоне от 0 до 65535 с шагом 4096. По умолчанию используется значение 32768.  

Шаг 1:	Отключите все порты на коммутаторах.  
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20150145-1.jpg)  

Аналогично для S1 и S3. 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab7/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2021-10-2022%20150348.jpg)





Шаг 2:	Настройте подключенные порты в качестве транковых.
Шаг 3:	Включите порты F0/2 и F0/4 на всех коммутаторах.
Шаг 4:	Отобразите данные протокола spanning-tree.











