##### Установка secret
kubectl apply -f .\hw-3\manifests\secret.yaml

##### Установка базы данных
helm install otus-hw-3-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-3\values.yaml

##### Установка оставшихся манифестов
kubectl apply -f .\hw-3\manifests

Коллекция запросо приложена в otus-homework.postman_collection.json