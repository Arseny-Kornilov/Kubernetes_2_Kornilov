# Домашнее задание к занятию «Сетевое взаимодействие в Kubernetes»
### Задание 1: Настройка Service (ClusterIP и NodePort)

#### Задача

Развернуть приложение из двух контейнеров (nginx и multitool) и обеспечить доступ к ним:

- Внутри кластера через ClusterIP.

- Снаружи через NodePort.

#### Шаги выполнения

1. Создать Deployment с двумя контейнерами:
 
 - nginx (порт 80).
 
 - multitool (порт 8080).
 
 - Количество реплик: 3.

2. Создать Service типа ClusterIP, который:

 - Открывает nginx на порту 9001.

 - Открывает multitool на порту 9002.

3. Проверить доступность изнутри кластера:

``` 
 kubectl run test-pod --image=wbitt/network-multitool --rm -it -- sh
 curl <service-name>:9001 # Проверить nginx
 curl <service-name>:9002 # Проверить multitool
```

4. Создать Service типа NodePort для доступа к nginx снаружи.

5. Проверить доступ с локального компьютера:

 ```
 curl <node-ip>:<node-port> или через браузер.
```
#### Что сдать на проверку

- Манифесты:
```
deployment-multi-container.yaml
service-clusterip.yaml
service-nodeport.yaml
```
- Скриншоты проверки доступа (curl или браузер).

- - - - -

### Решение:
<img width="1561" height="610" alt="image" src="https://github.com/user-attachments/assets/0d30dbd2-9c5b-43ce-9a7a-24d734909587" />
<img width="1676" height="1165" alt="image" src="https://github.com/user-attachments/assets/7babcab3-8655-45a3-9505-ff10d425cee4" />
<img width="863" height="475" alt="image" src="https://github.com/user-attachments/assets/92159dd3-2ea6-46fb-8412-7e0ba0b669c7" />
<img width="978" height="616" alt="image" src="https://github.com/user-attachments/assets/f5771d5a-7cc8-4c81-8c0d-d199718051de" />
<img width="1650" height="1137" alt="image" src="https://github.com/user-attachments/assets/0904258c-e3f3-41a0-9e37-bbdf00ce04d7" />




