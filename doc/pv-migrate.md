# refer:
[pv-migrate](https://github.com/utkuozdemir/pv-migrate/blob/master/USAGE.md)
[awx-operator/backup](https://github.com/ansible/awx-operator/blob/devel/roles/backup/README.md)
[awx-operator/restore](https://github.com/ansible/awx-operator/blob/devel/roles/restore/README.md)

# install pv-migrate

[install link](https://github.com/utkuozdemir/pv-migrate/blob/master/INSTALL.md)
# usage
tasks:
1. create target pvc 
2. create awxbackup resource
3. perform pv-migrate migrate data
4. find backupDirectory value and paste to awx-restore.yaml
5. perform awx-restore.yaml
6. 



1. create target pvc
    ```bash
    # create pvc on awx2
    k apply -f test-pvc.yaml
    ```

2. create awxbackup resource
    ```
    k apply -f backup.yaml
    ```

3. perform pv-migrate migrate data
    ```bash
    pv-migrate migrate \
    --source-namespace awx \
    --dest-namespace awx2 \
    awx-backup-claim pv-migrate2
    ```

4. find backupDirectory value and paste to awx-restore.yaml
    At target k8s - get backup_pvc
    ```bash
    kubectl get pvc -n awx2
    ```

    At awxbackup k8s get backup_dir
    ```bash
    kubectl get awxbackup -n awx awxbackup-2023-10-25  \
    -o jsonpath='{.status.backupDirectory}'
    ```
    Paste at awx-restore.yaml
    ```
    /backups/tower-openshift-backup-2023-10-26-024657
    ```
