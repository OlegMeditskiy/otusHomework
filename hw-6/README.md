##### Установка secret перед базой данных
kubectl apply -f .\hw-6\manifests\secret.yaml

##### Установка базы данных
helm install otus-hw-6-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f .\hw-6\values.yaml

##### Установка оставшихся манифестов
kubectl apply -f .\hw-6\manifests

Коллекция запросов приложена в [auth-service.postman_collection.json](auth-service.postman_collection.json)
