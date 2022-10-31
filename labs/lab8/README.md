## Лабораторная работа - Настройка DHCP


<details><summary>1. Настройка DHCPv4</summary>
  
### Топология

![Лабораторная работа](https://github.com/elborisova3009/otus-networks/blob/master/labs/lab8/%D0%A1%D0%BA%D1%80%D0%B8%D0%BD%D1%88%D0%BE%D1%82%2031-10-2022%20132045.jpg)  

### Таблица адресации

###	Таблица VLAN

###	Задачи

<details><summary>Часть 1. Создание сети и настройка основных параметров устройства.</summary> 

</details>   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.


<details><summary>Часть 2. Настройка и проверка двух серверов DHCPv4 на R1</summary>  

   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>

<details><summary>Часть 3. Настройка и проверка DHCP-ретрансляции на R2.</summary> 


   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>
  
    1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

  

</details>

_____________________________________


<details><summary>2. Настройка DHCPv6</summary>

   1. First item must be preceeded with an empty line.
   1. Markdown renders **perfectly**.
   1. Extra item.

</details>

_____________________________________


```
conf t
ip default-gateway 172.17.127.254
VLAN 99
name Managment
int Vlan 99
ip add 172.17.0.2 255.255.128.0
no shutdown
VLAN 10
name Workplaces
```

