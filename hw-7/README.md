##### Установка secret перед базой данных
kubectl apply -f .\hw-7\manifests\secret.yaml

##### Установка базы данных
helm install auth-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-7\values.yaml; helm install billing-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-7\values.yaml; helm install order-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-7\values.yaml; helm install notification-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-7\values.yaml;

##### Установка кафка
kubectl apply -f .\hw-7\manifests\kafka
По готовности кафки
kubectl exec -it deployment/kafka-deployment -- /bin/bash
kafka-topics --create --topic orders --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic payments --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic users --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic billing-account --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 
exit

##### Установка оставшихся манифестов
kubectl apply -f .\hw-7\manifests --recursive

Коллекция запросов приложена в [otus-homework-7.postman_collection.json](otus-homework-7.postman_collection.json)
