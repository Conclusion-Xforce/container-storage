# Stateful set

## Step 1 - Create a stateful set for mysql
* Image: quay.io/fedora/mysql-80
* Environment variable: MYSQL_ROOT_PASSWORD with the value of test
* Per pod the persistent volume needs to be mounted on `/var/lib/mysql` (15GB)
* During an update pods need to be restart one by one manually
* The used storage class should be `managed-csi`.

## Step 2 - Test wether the update strategy is working as expect
Update the mysql image version to `20240508`

## Resources

* [Statefulset references | Kubernetes Docs](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
