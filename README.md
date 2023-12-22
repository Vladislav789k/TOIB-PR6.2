# TOIB-PR6.2
# Практическое задание №6. Настройка протокола GRE

Выполнил Карпейкин В.А., группа ББМО-02-23

## Общая структурная схема сети

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/1ccd2b7b-a16e-4f20-98d7-54a7ff5ea817)
![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/9940a23e-8bbc-4140-a3e2-c31bb8c6d4be)


# Часть 1: Проверка подключения маршрутизатора

## Шаг 1: Определение IP-адреса порта S0/0/0 на маршрутизаторе RA.

```
show ip int br
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/050474e8-10a1-4510-851e-476ebd47ca41)


## Отправка эхо-запроса с RB на RA

```
ping 64.103.211.2
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/13c7d50d-35dd-4136-9dab-6bc959a546f6)


## Шаг 2: Определение IP-адреса на ПК А.

```
ipconfig
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/346c7cd5-bb62-4e08-b212-1748a22f5eea)


## Шаг 3: Отправка эхо-запроса до настройки туннеля GRE

```
ping 192.168.1.2
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/2ea76a20-d10f-4b81-8770-bf6089c08d79)



# Часть 2: Настройка туннеля GRE

## Шаг 1:  Настройка туннеля GRE на маршрутизаторе RA

```
enable

conf t

int tunnel 0

ip address 10.10.10.1 255.255.255.252

tunnel source s0/0/0

tunnel destination 209.165.122.2

tunnel mode gre ip
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/ac37e3af-e24c-4d11-aa3a-34787d74f826)


## Шаг 2: Настройка туннеля GRE на маршрутизаторе RB.

```
en

conf t

int tunnel 0

ip address 10.10.10.2 255.255.255.252

tunnel source s0/0/0

tunnel destination 64.103.211.2

tunnel mode gre ip

```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/9d3f3820-f9f0-4918-8c33-caa1b81ec557)


## Шаг 3: Настройте маршрут для частного IP-трафика.

```
conf t

ip route 192.168.2.0 255.255.255.0 10.10.10.2
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/10eeb0aa-b05f-441c-ad29-52c25564f46b)


```
no shutdown

exit

ip route 192.168.1.0 255.255.255.0 10.10.10.1
```

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/0bbae68d-754f-4211-9943-41cd5602a101)


# Часть 3: Проверка подключения маршрутизатора

## Шаг 1: Отправка эхо-запроса с ПК B на ПК А после настройки GRE туннеля

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/c7ffedcc-08e7-4529-b482-e5dd33164927)


## Шаг 2: Трассировка от ПК А до ПК В

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/0bdb7699-ed36-4ad1-9986-8bb0dfb24c65)

## Проверка правильности выполнения работы

![image](https://github.com/Vladislav789k/TOIB-PR6.2/assets/71137501/f1f4fe89-0d37-490c-b12a-cfcb008cfbf5)
