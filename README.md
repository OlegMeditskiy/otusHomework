##### Установка манифестов одной командой
kubectl apply -f manifests

##### Проверка health
curl http://arch.homework/health

##### Проверка перезаписи пути с любым именем студента
curl http://arch.homework/otusapp/oleg/health
curl http://arch.homework/otusapp/maxim/health