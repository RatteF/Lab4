# Lab4
Zunächst muss ein Azure Kubernetes-Cluster erstellt werden. Dafür müssen im Terminal folgende Befehle eingegeben werden:
```az login```
Dann mit seinen Azure Daten anmelden.
```az group create -n <IhrName> --location westeurope```
```az aks create --resource-group <IhrName> --name <IhrName> --node-count 1 --generate-ssh-keys```
```az aks install-cli```
```az aks get-credentials -g <IhrName> -n <IhrName>```
Anschließend können die Files gedownloadet werden. Wenn dies getan wurde muss mit dem Befehl ```cd Ihr\Pfad``` in den Ordner mit den Dateien navigiert werden.
Nun müssen nacheinander folgende Befehle ausgeführt werden:
```kubectl apply -f mysql-secret.yaml
kubectl apply -f mysql-pv-pvc.yaml
kubectl apply -f mysql-statefulset.yaml
kubectl apply -f mysql-service.yaml
kubectl apply -f wordpress-pv-pvc.yaml
kubectl apply -f wordpress-deployment.yaml```
Jetzt sollte mit dem Befehl ```kubectl get svc wordpress-service``` nachgeschaut werden, was die "External-IP" ist. Bis diese erscheint könnten ein paar Minuten vergehen.
Sobald eine IP angezeigt wird, kann der Link http://"IhreExternalIP":30007 in einem Browserfenster eingegeben werden und es erscheint die Wordpress Seite.

Folgend weitere Bilder:
Cluster Status mit der URL: https://portal.azure.com/#@fhwn.ac.at/resource/subscriptions/f27379d5-931b-49b4-a4a8-a7490d71fc75/resourceGroups/grasnick23/providers/Microsoft.ContainerService/managedClusters/grasnick23/overview
![cluster status neu erstellt](https://github.com/RatteF/Lab4/assets/83348757/8fc500e0-c5c9-47bc-a649-b0e232be7a45)
Laufendes Cluster
![laufendes kluster](https://github.com/RatteF/Lab4/assets/83348757/bcdbeafe-ac88-4373-a63a-143887fa3e4c)

