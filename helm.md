

MySQL via HELM

```
# install
helm install stable/mysql --name mysql0

# open shell
export MYSQL_ROOT_PASSWORD=$(kubectl get secret mysql0 -o jsonpath="{.data.mysql-root-password}" | base64 --decode; echo)
kubectl exec -it `kubectl get po | grep mysql0 | cut -f1 -d' '` -- mysql -u root -p$MYSQL_ROOT_PASSWORD

# uninstall
helm delete mysql0

```
PostGres via HELM
```
# install
helm install stable/postgresql --name postgres
export PGPASSWORD=$(kubectl get secret postgres-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)

# open shell
kubectl exec -it `kubectl get po | grep postgres | cut -f1 -d' '` --  psql postgresql://postgres:$PGPASSWORD@127.0.0.1:5432

# uninstall
helm delete postgres
```


Redis via HELM
```
helm install stable/redis --name redis
kubectl exec -it `kubectl get po | grep redis-slave | cut -f1 -d' '` redis-cli
```

