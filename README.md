# Кластеризация и балансировка нагрузки Евдокимов Евгений Игоревич  

### Задание 

## Задание 1
Запустите два simple python сервера на своей виртуальной машине на разных портах
Установите и настройте HAProxy, воспользуйтесь материалами к лекции по ссылке
Настройте балансировку Round-robin на 4 уровне.
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.

## Задание 2
Запустите три simple python сервера на своей виртуальной машине на разных портах
Настройте балансировку Weighted Round Robin на 7 уровне, чтобы первый сервер имел вес 2, второй - 3, а третий - 4
HAproxy должен балансировать только тот http-трафик, который адресован домену example.local
На проверку направьте конфигурационный файл haproxy, скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него.

### Решение

Задание 1

Наполнение файла haproxy.cfg

```
global
    log /dev/log local0
    log /dev/log local1 notice
    daemon

defaults
    log global
    mode tcp
    option tcplog
    timeout connect 5s
    timeout client  50s
    timeout server  50s

frontend frontend_http
    bind *:8080
    default_backend backend_servers

backend backend_servers
    balance roundrobin
    server server1 127.0.0.1:8888 check
    server server2 127.0.0.1:9999 check
```
![скриншот с демонстрацией работы robin](Robin.png)


### Задание 2



