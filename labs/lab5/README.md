## Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH

### Топология
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20121306.jpg)

### 	Таблица адресации
![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20120646-1.jpg)

### 	Задачи
Часть 1. Настройка основных параметров устройства
Часть 2. Настройка маршрутизатора для доступа по протоколу SSH
Часть 3. Настройка коммутатора для доступа по протоколу SSH
Часть 4. SSH через интерфейс командной строки (CLI) коммутатора

### 	Часть 1. Настройка основных параметров устройств

Шаг 1. Создаю в CPT сеть согласно топологии.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20130805-1.jpg) 

Шаг 2. Выполнение инициализации и перезагрузка устройств в CPT не предполагается.

Шаг 3. Настрою маршрутизатор R1 согласно заданному алгоритму.  
Конфиг:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%2016282-1.jpg)

Шаг 4. Настрою компьютер PC-A согласно заданию.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20131018.jpg)  

Шаг 5. Проверю подключение к сети - пропингую с PC-A маршрутизатор R1. Пинг успешен.    

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20131147.jpg)  

### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH  

Согласно заданию:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20170218-1.jpg)  
Конфиг выглядит так: 

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20165839.jpg) 

Шаг 6. Устанавлю соединение с маршрутизатором R1 по протоколу SSH, используя логин ssh_admin и пароль enAdm1nP@55.  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20170735.jpg)

### Часть 3. Настройка коммутатора для доступа по протоколу SSH

Шаги 1-2 аналогичны настройке маршрутизатора (логин и пароль использовала те же).  
Конфиг:  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20172338.jpg)  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20172710.jpg)  

Show Run:

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20175837.jpg)

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20175848.jpg)


Шаг 3. Установлю соединение с коммутатором S1 по протоколу SSH, используя логин ssh_admin и пароль enAdm1nP@55.  

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20172910.jpg)


### Часть 4. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора

Шаг 1. Посмотрю доступные параметры для клиента SSH в Cisco IOS.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20173913.jpg)  


Шаг 2. Установлю с коммутатора S1 соединение с маршрутизатором R1 по протоколу SSH.

![alt text](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab5/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2011-10-2022%20175734.jpg)

Вопрос.  
Какие версии протокола SSH поддерживаются при использовании интерфейса командной строки?  *SSH1 ,SSH2*  

### Вопрос для повторения

Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?  
*Настроить доступ по SSH, создать уникальных пользователей (команда username).*



































