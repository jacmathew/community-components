# How to supress alerts - VeleroBackupTakesTooLong

Velero is an open source tool to safely backup and restore, perform disaster recovery, and migrate Kubernetes cluster resources and persistent volumes. using velero the recommended practice is to take backups every hour. However at times backups will get stuck and become partial and the alermanager will start complaining about unsucessful backups which needs to be addressed. The below guide helps in clearing such alerts. A typical alerts looks like below...

![velerobackupAlert](https://user-images.githubusercontent.com/29113813/148930107-6ca05f08-e7ed-427f-a527-8363d33019c2.png)

Below are the steps involed in clearing this alerts from alert manager.

1. Login to the cluster - (export the KUBECONFIG)

2. List velero backups - `velero backups get` - You will be able to see the the list of backups as below.

![Velero backup get](https://user-images.githubusercontent.com/29113813/148933520-54036a8a-8a1c-4992-9fa5-37bc440476f7.png)

3. You can identify the partial backups from the below command. Esure you have complete backups in the system post the partial/failed backups.

4. Now delete the failed/partial backup using `velero delete backup <backup_name>`

5. Once the backup is deleted delete the velero pod as well using command `kubectl delete pod velero-85c75b5db-srt8k -n velero`

6. Once deleted the pod will get scheduled again and alert will get cleared.


