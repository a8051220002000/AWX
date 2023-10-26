# delete a awx resource. 
include  resource awx pvc awxrestore

```bash
 k delete awx -n awx2 awx-restore 
 k delete awxrestores.awx.ansible.com -n awx2 awx
 k delete pvc -n awx2 awx-backup-claim postgres-13-awx-postgres-13-0
```

```bash
 k get secret -n awx2|grep -e ^awx|awk '{print $1}'
 k get secret -n awx2|grep -e ^awx |awk '{print $1}'|xargs kubectl delete secret -n awx2 {}
```

