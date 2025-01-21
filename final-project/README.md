##### Установка prometheus
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus -f ./final-project/prometheus/prometheus.yaml
Если нужно проверить прометеус
kubectl port-forward service/prometheus-server 9090:80

##### Установка grafana и получение пароля - логин admin
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
Если нужно проверить графану
kubectl port-forward service/grafana 3000:80
Доступ к prometheus по http://prometheus-server:80
id дашбордов для создания - 19004

##### Установка secret перед базой данных
kubectl apply -f ./final-project/manifests/secret.yaml

##### Установка базы данных
helm install auth-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install billing-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install order-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install delivery-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install stock-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml && helm install notification-postgresql oci://registry-1.docker.io/bitnamicharts/postgresql -f ./final-project/values.yaml

##### Установка кафка
kubectl apply -f ./final-project/kafka
По готовности кафки
kubectl exec -it deployment/kafka-deployment -- /bin/bash
kafka-topics --create --topic order-command --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 && kafka-topics --create --topic users --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1
exit

##### Установка оставшихся манифестов
kubectl apply -f ./final-project/manifests --recursive

Коллекция запросов приложена в [final-project.postman_collection.json](final-project.postman_collection.json)