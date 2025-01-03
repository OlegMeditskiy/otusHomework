##### Установка secret перед базой данных
kubectl apply -f ./hw-9/manifests/secret.yaml

##### Установка базы данных
helm install auth-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-9\values.yaml; helm install billing-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-9\values.yaml; helm install order-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-9\values.yaml; helm install delivery-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-9\values.yaml; helm install inventory-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-9\values.yaml;
helm install auth-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./hw-9/values.yaml; helm install billing-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./hw-9/values.yaml; helm install order-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./hw-9/values.yaml; helm install delivery-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./hw-9/values.yaml; helm install inventory-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./hw-9/values.yaml;
##### Установка кафка
kubectl apply -f ./hw-9/kafka
По готовности кафки
kubectl exec -it deployment/kafka-deployment -- /bin/bash
kafka-topics --create --topic order-command --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic payments --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic users --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic billing-account --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic stock --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic delivery --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
exit

##### Установка оставшихся манифестов
kubectl apply -f ./hw-9/manifests --recursive

Коллекция запросов приложена в [homework 9 test.postman_collection.json](homework%209%20test.postman_collection.json)