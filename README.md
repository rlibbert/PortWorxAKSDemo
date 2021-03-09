# PortWorxAKSDemo
Sign into PW portal.

Create Blob storage in Azure

Grab the portwox helm repo

   helm repo add portworx http://charts.portworx.io/ && helm repo update 
   
Go back to the portal and enter the storage class name (in this case portworxbu)

Use the generated helm cmd to install:

    helm install px-backup portworx/px-backup --namespace px-backup --create-namespace --version 1.2.2 --set persistentStorage.enabled=true,persistentStorage.storageClassName="portworxbu"


Output:

NAME: px-backup
LAST DEPLOYED: Mon Feb 22 09:42:06 2021
NAMESPACE: px-backup
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
Your Release is named: "px-backup"
PX-Backup deployed in the namespace: px-backup

--------------------------------------------------
Monitor PX-Backup Install:
--------------------------------------------------
Wait for px-backup status to be in "Completed" state.

    kubectl get po --namespace px-backup -ljob-name=pxcentral-post-install-hook  -o wide | awk '{print $1, $3}' | grep -iv error

--------------------------------------------------
Access PX-Backup UI:
--------------------------------------------------
Using port forwarding:

    kubectl port-forward service/px-backup-ui 8080:80 --namespace px-backup

To access PX-Backup:  http://localhost:8080
Login with the following credentials:

    Username: admin
    Password: admin

For more information: https://github.com/portworx/helm/blob/master/charts/px-backup/README.md
