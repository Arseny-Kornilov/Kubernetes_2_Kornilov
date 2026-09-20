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

![1](https://github.com/Ivan-Shkutov/kuber_1.4/blob/main/jpg/1.png)

![2](https://github.com/Ivan-Shkutov/kuber_1.4/blob/main/jpg/2.png)

![3](https://github.com/Ivan-Shkutov/kuber_1.4/blob/main/jpg/3.2.png)

![4](https://github.com/Ivan-Shkutov/kuber_1.4/blob/main/jpg/3.3.png)

![5](https://github.com/Ivan-Shkutov/kuber_1.4/blob/main/jpg/3.png)


```
1. Проверяем статус Minikube:
minikube status

2. Запускаем Minikube (если не запущен):
minikube start

Minikube создаёт локальную виртуальную машину с Kubernetes.
После запуска API-сервер будет доступен, kubectl автоматически настроится.

3. Проверяем, что kubectl видит ноды:
kubectl get nodes

4. Применяем Deployment:
kubectl apply -f deployment-multi-container.yaml

5. Проверяем поды:
kubectl get pods

6. Применяем Service:
kubectl apply -f service-clusterip.yaml

7. Проверяем сервис:
kubectl get svc

8. Создаём временный тестовый pod:
kubectl run test-pod --image=wbitt/network-multitool --rm -it -- sh

9. Проверяем доступ к сервису:
curl multi-container-clusterip:9001
curl multi-container-clusterip:9002

10. Применяем Service:
kubectl apply -f service-nodeport.yaml

11. Проверяем сервис:
kubectl get svc

12. Проверяем curl с локального компьютера:
curl http://192.168.49.2:30080
```
