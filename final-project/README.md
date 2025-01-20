##### Установка secret перед базой данных
kubectl apply -f ./final-project/manifests/secret.yaml

##### Установка базы данных
helm install auth-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install billing-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install order-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install delivery-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install stock-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install notification-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml

##### Установка прометеуса
helm install otus-prometheus prometheus-community/kube-prometheus-stack -f ./final-project/prometheus/prometheus.yaml
##### Установка кафка
kubectl apply -f ./final-project/kafka
По готовности кафки
kubectl exec -it deployment/kafka-deployment -- /bin/bash
kafka-topics --create --topic order-command --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic users --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
exit


##### Установка оставшихся манифестов
kubectl apply -f ./final-project/manifests --recursive

Коллекция запросов приложена в [homework 9 test.postman_collection.json](homework%209%20test.postman_collection.json)