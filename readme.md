# Test mysql operator on k8s
I'm testing Bitpoke, Oracle MySQL Operator, and Percona Operator for MySQL (based on PXC). After testing 3 operators Mysql, I choise Percona Operator for MySQL (based on PXC), the best tool MySQL operator for my preference. Many features and minimal bug, so i chose this. 

Refrence doc : [link](https://docs.percona.com/percona-operator-for-mysql/pxc/index.html)

> Notes:
- If the cluster in remove pvc not remove automatic.
- If pcv is not delete, when the cluster is recreated with the same template. The old PVC will be reused and the previously existing database will be restored.


# Setup operator
- Apply operator on k8s 
```
kubectl -n (namespace) apply -f bundle-setup-oprator.yaml
```
- Check operator status
```
kubectl -n (namespace) get all -o wide
```

# Setup cluster
Enter Cluster-config and choose backup destination 
> Example using pvc backup
- Enter `backup-using-pvc` directory
```
cd backup-using-pvc
```
- Apply credential access DB \
Before apply, update value secret config
```
kubectl -n (namespace) apply -f secrets.yaml
```
- Apply cluster config mysql database
```
kubectl -n (namespace) apply -f cr-minimal.yaml

```
- Apply backup config for mysql database cluster
```
kubectl -n (namespace) apply -f backup-cr.yaml
```
## If you want to restore a backup to the database, use `restore-db-cr.yaml`. 
Before apply, update value.
```
kubectl -n (namespace) apply -f restore-db-cr.yaml

```

# backup and restore
https://github.com/percona/percona-xtradb-cluster-operator/blob/main/deploy/backup/README.md

# setup cluster template doc
https://github.com/percona/percona-xtradb-cluster-operator/tree/main/deploy \
https://docs.percona.com/percona-operator-for-mysql/pxc/minikube.html