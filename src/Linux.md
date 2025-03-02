1. [Part 1. Инструмент ipcalc](#Part-1.-Инструмент-ipcalc)
2. [Part 2. Статическая маршрутизация между двумя машинами](#Part-2.-Статическая-маршрутизация-между-двумя-машинами)
3. [Part 3. Утилита iperf3](#Part-3.-Утилита-iperf3)
4. [Part 4. Сетевой экран](#Part-4.-Сетевой-экран)

## Part 1. Инструмент ipcalc ##

-  Устанавливаем ipcalc
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.png"><br>


### 1.1 Сети и маски ###
- Адрес сети 192.167.38.54/13
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.1.png"><br>

#### Перевод маски 255.255.255.0 в префиксную и двоичную запись, /15 в обычную и двоичную, 11111111.11111111.11111111.11110000 в обычную и префиксную ####

- 255.255.255.0 в префиксной форме - /24, а в двоичной - 11111111.11111111.11111111.00000000
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.2.png"><br>

- /15 - 11111111.11111110.00000000.00000000
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.3.png"><br>

- 11111111.11111111.11111111.11110000 - /28 или 255.255.255.240
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.4.png"><br>


#### Минимальный и максимыльный хост в сети 12.167.38.4 при масках: /8, 11111111.11111111.00000000.00000000, 255.255.254.0 и /4 ####

- для адреса 12.167.38.4 при маске /8 минимальный хост - 12.0.0.1, максимальный хост 12.255.255.254
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.5.png"><br>

- при маске 11111111.11111111.00000000.00000000 минимальный хост - 12.167.0.1, максимальный хост 12.167.255.254
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.6.png"><br>

- 255.255.254.0 минимальный хост - 12.167.38.1, максимальный хост 12.167.39.254
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.7.png"><br>

- /4 минимальный хост - 0.0.0.1, максимальный хост 15.255.255.254
<img title="title" alt="OS installation screenshot" src="./screens/part1/1.1.8.png"><br>

### 1.2 localhost ###

#### Определим и запишем в отчёт, можно ли обратиться к приложению, работающему на localhost, со следующими IP: 194.34.23.100, 127.0.0.2, 127.1.0.1, 128.0.0.1 ####

- 194.34.23.100 - нет
- 127.0.0.2 - да
- 127.1.0.1 - да
- 128.0.0.1 - нет

### 1.3 Диапазоны и сегменты сетей ###

1. Какие из перечисленных IP можно использовать в качестве публичного, а какие только в качестве частных: 10.0.0.45, 134.43.0.2, 192.168.4.2, 172.20.250.4, 172.0.2.1, 192.172.0.1, 172.68.0.2, 172.16.255.255, 10.10.10.10, 192.169.168.1

- 10.0.0.45 - private
- 134.43.0.2 - public
- 192.168.4.2 - private
- 172.20.250.4 - private
- 172.0.2.1 - public
- 192.172.0.1 - piblic
- 172.68.0.2 - public
- 172.16.255.255 - private
- 10.10.10.10 - private
- 192.169.168.1 - public

2. Какие из перечисленных IP-адресов шлюза возможны у сети 10.10.0.0/18: 10.0.0.1, 10.10.0.2, 10.10.10.10, 10.10.100.1, 10.10.1.255

- 10.0.0.1 - нет
- 10.10.0.2 - да
- 10.10.10.10 - да
- 10.10.100.1 - нет
- 10.10.1.255 - да

## Part 2. Статическая маршрутизация между двумя машинами ##

- С помощью команды `ip a` посмотрим существующие сетевые интерфейсы
<img title="title" alt="OS installation screenshot" src="./screens/part2/2.1.png"><br>
<img title="title" alt="OS installation screenshot" src="./screens/part2/2.2.png"><br>

Описать сетевой интерфейс, соответствующий внутренней сети, на обеих машинах и задать следующие адреса и маски: ws1 - 192.168.100.10, маска /16, ws2 - 172.24.116.8, маска /12

<img title="title" alt="OS installation screenshot" src="./screens/part2/2.3.png"><br>

Выполним команду `netplan apply` для перезапуска сервиса сети
<img title="title" alt="OS installation screenshot" src="./screens/part2/2.4.png"><br>

### 2.1 Добавление статического маршрута вручную ###

#### Добавь статический маршрут от одной машины до другой и обратно при помощи команды вида `ip r add.` ####

<img title="title" alt="OS installation screenshot" src="./screens/part2/2.5.png"><br>

#### Пропингуй соединение между машинами ####

<img title="title" alt="OS installation screenshot" src="./screens/part2/2.6.png"><br>

### 2.2 Добавление статического маршрута с сохранением ###

#### Перезапусти машину ####

#### Добавь статический маршрут от одной машины до другой с помощью файла etc/netplan/00-installer-config.yaml. ####

<img title="title" alt="OS installation screenshot" src="./screens/part2/2.7.png"><br>

#### Пропингуй соединение между машинами. ####

<img title="title" alt="OS installation screenshot" src="./screens/part2/2.8.png"><br>

## Part 3. Утилита iperf3 ##

### 3.1. Скорость соединения ###

#### Переведи и запиши в отчёт: 8 Mbps в MB/s, 100 MB/s в Kbps, 1 Gbps в Mbps. ####
#### 8 Mbps = (Mbps / 8) = 1 MB/s ####
#### 100 MB/s = (MB/s * 8 * 1024) = 819200 Kbps ####
#### 1 Gbps = (Gbps * 1000) = 1000 Mbps #### 

### 3.2. Утилита iperf3 ###

#### Измерь скорость соединения между ws1 и ws2. ####

- На машине ws2 запускаем сервер утилиты ipref3 с помощью команды ipref3 -s, для того чтоб машина принимала входящее соединение.
<img title="title" alt="OS installation screenshot" src="./screens/part3/3.1.png"><br>

- На машине ws1 запускаем клиент утилиты ipref3 для отправки данных на машину ws1 с помощью команды ipref3 -c 172.24.116.8
<img title="title" alt="OS installation screenshot" src="./screens/part3/3.2.png"><br>


## Part 4. Сетевой экран ##

### 4.1. Утилита iptables ###

Нужно создать файл `/etc/firewall.sh` и добавить в файл подряд следующие правила:

1) На ws1 примени стратегию, когда в начале пишется запрещающее правило, а в конце пишется разрешающее правило (это касается пунктов 4 и 5).

2) На ws2 примени стратегию, когда в начале пишется разрешающее правило, а в конце пишется запрещающее правило (это касается пунктов 4 и 5).

3) Открой на машинах доступ для порта 22 (ssh) и порта 80 (http).

4) Запрети echo reply (машина не должна «пинговаться», т. е. должна быть блокировка на OUTPUT).

5) Разреши echo reply (машина должна «пинговаться»).

![linux_network](./screens/part4/4.1.png)

- в отчете поместить скрины с запуском обоих файлов
![linux_network](./screens/part4/4.2.png)
![linux_network](./screens/part4/4.3.png)

- В отчёте опиши разницу между стратегиями, применёнными в первом и втором файлах.

- - На **ws1** весь трафик изначально блокируется (**DROP**), после чего разрешаются только определённые подключения (**ACCEPT**), и всё, что не соответствует установленным правилам, отклоняется. На **ws2**, наоборот, весь трафик сначала разрешается (**ACCEPT**), а затем блокируются только определённые подключения (**DROP**), в результате чего остаётся доступным всё, что не подпадает под запрет.

### 4.2. Утилита nmap ###

![linux_network](./screens/part4/4.4.png)
![linux_network](./screens/part4/4.5.png)

## Part 5. Статическая маршрутизация сети ##

### 5.1 Настройка адресов машин ###

настройка файла netplan согласно рисунку

r1
![linux_network](./screens/part5/5.1.png)

r2
![linux_network](./screens/part5/5.2.png)

ws11
![linux_network](./screens/part5/5.3.png)

ws21
![linux_network](./screens/part5/5.4.png)

ws22
![linux_network](./screens/part5/5.5.png)

- Перезапустиv сервис сети. Если ошибок нет, командой ip -4 a проверь, что адрес машины задан верно.

ws11
![linux_network](./screens/part5/5.6.png)

ws21
![linux_network](./screens/part5/5.7.png)

ws22
![linux_network](./screens/part5/5.8.png)

r1
![linux_network](./screens/part5/5.9.png)

r2
![linux_network](./screens/part5/5.10.png)

пропингуй ws22 с ws21
![linux_network](./screens/part5/5.11.png)

Аналогично пропингуй r1 с ws11.
![linux_network](./screens/part5/5.12.png)

### 5.2. Включение переадресации IP-адресов ###

Для включения переадресации IP выполни команду на роутерах:
`sudo sysctl -w net.ipv4.ip_forward=1`

![linux_network](./screens/part5/5.13.png)

Открыть файл /etc/sysctl.conf и добавить в него следующую строку: `net.ipv4.ip_forward = 1`

![linux_network](./screens/part5/5.14.png)

### 5.3. Установка маршрута по умолчанию ###

Настраиваем маршрут по-умолчанию (шлюз) для рабочих станций. Для этого добавляем gateway4: ip роутера в файле конфигураций etc/netplan/00-installer-config.yaml
- ws11
![linux_network](./screens/part5/5.15.png)

- ws21
![linux_network](./screens/part5/5.16.png)

- ws22
![linux_network](./screens/part5/5.17.png)

Вызовите ip r и покажите, что маршрут добавлен в таблицу маршрутизации

- ws11
![linux_network](./screens/part5/5.18.png)
- ws21
![linux_network](./screens/part5/5.19.png)
- ws22
![linux_network](./screens/part5/5.20.png)


Пропинговать с ws11 роутер r2 и показать на r2, что пинг доходит. Для этого использовать команду: `tcpdump -tn -i enp0s9:`

![linux_network](./screens/part5/5.22.png)
![linux_network](./screens/part5/5.23.png)

### 5.4. Добавление статических маршрутов ###

- Добавь в роутеры r1 и r2 статические маршруты в файле конфигураций. Пример для r1 маршрута в сетку 10.20.0.0/26:

![linux_network](./screens/part5/5.24.png)
![linux_network](./screens/part5/5.25.png)

- С помощью ip r проверяем настройки на роутерах
![linux_network](./screens/part5/5.26.png)
![linux_network](./screens/part5/5.27.png)

- Запустить команды на ws11: `ip r list 10.10.0.0/[маска сети]` и `ip r list 0.0.0.0/0` В отчёт поместить скрин с вызовом и выводом использованных команд:
![linux_network](./screens/part5/5.28.png)

- Маршрут по умолчанию имеет более низкий приоритет, а для 10.10.0.0/18 был найден подходящий маршрут в таблице маршрутизации, соответственно и был использован

### 5.5. Построение списка маршрутизаторов ###

- Запустить на r1 команду дампа: tcpdump -tnv -i enp0s9
![linux_network](./screens/part5/5.29.png)

- При помощи утилиты traceroute построить список маршрутизаторов на пути от ws11 до ws21:
![linux_network](./screens/part5/5.30.png)

Traceroute работает, отправляя UDP-пакеты с увеличивающимся TTL и фиксируя ICMP-ответы "Time Exceeded" от маршрутизаторов. По скрину видно, что пакеты отправляются от 10.10.0.2 к 10.20.0.10, но обрываются на 10.10.0.1, который отправляет ICMP-ответ. Это говорит о том, что маршрутизация дальше либо отсутствует, либо трафик фильтруется. Traceroute помогает определить этот маршрут.

### 5.6. Использование протокола ICMP при маршрутизации ###

- Запусти на r1 перехват сетевого трафика, проходящего через eth0 с помощью команды: `tcpdump -n -i eth0 icmp`

- Пропинговать с ws11 несуществующий IP (например, 10.30.0.111) с помощью команды: `ping -c 1 10.30.0.111`
![linux_network](./screens/part5/5.31.png)
![linux_network](./screens/part5/5.32.png)

## Part 6. Динамическая настройка IP с помощью DHCP ##

- Для r2 настрой в файле /etc/dhcp/dhcpd.conf конфигурацию службы DHCP:
 1. Укажи адрес маршрутизатора по умолчанию, DNS-сервер и адрес внутренней сети.
 ![linux_network](./screens/part6/6.1.png)

 2. В файле resolv.conf пропиши nameserver 8.8.8.8.
  ![linux_network](./screens/part6/6.2.png)

  - Перезагрузи службу DHCP командой `systemctl restart isc-dhcp-server`.
  ![linux_network](./screens/part6/6.3.png)

  - Машину ws21 перезагрузить при помощи reboot и через ip a показать, что она получила адрес. Также пропинговать ws22 с ws21.
  ![linux_network](./screens/part6/6.4.png)
  ![linux_network](./screens/part6/6.5.png)

  - Укажи MAC-адрес у ws11, для этого в etc/netplan/00-installer-config.yaml надо добавить строки: macaddress: 10:10:10:10:10:BA, dhcp4: true.
  ![linux_network](./screens/part6/6.6.png)

  - Для r1 настрой аналогично r2, но сделай выдачу адресов с жесткой привязкой к MAC-адресу (ws11). Проведи аналогичные тесты.
  ![linux_network](./screens/part6/6.7.png)
  ![linux_network](./screens/part6/6.8.png)
  ![linux_network](./screens/part6/6.9.png)

  - Укажи MAC-адрес у ws11, для этого в etc/netplan/00-installer-config.yaml надо добавить строки: macaddress: 10:10:10:10:10:BA, dhcp4: true.
  ![linux_network](./screens/part6/6.6.png)
  ![linux_network](./screens/part6/6.4.png)
  ![linux_network](./screens/part6/6.10.png)

  - Запроси с ws21 обновление IP-адреса.
  `ip a`
  ![linux_network](./screens/part6/6.12.png)
  ![linux_network](./screens/part6/6.13.png)

  Пользовался опциями:
  `-r: Очистка IP-адреса`
  `-v: Показ подробного вывода`
