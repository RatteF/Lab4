# Lab4

## Implementierung

Zunächst muss ein Azure Kubernetes-Cluster erstellt werden. Dafür müssen im Terminal folgende Befehle eingegeben werden:
```az login```
Dann mit seinen Azure Daten anmelden.

```az group create -n <IhrName> --location westeurope```

```az aks create --resource-group <IhrName> --name <IhrName> --node-count 1 --generate-ssh-keys```

```az aks install-cli```

```az aks get-credentials -g <IhrName> -n <IhrName>```

Anschließend können die Files gedownloadet werden.

Jetzt müssen die hostPaths in den Files "wordpress-pv-pvc.yaml" & "mysql-pv-pvc.yaml" angepasst werden.

Wenn dies getan wurde muss mit dem Befehl ```cd Ihr\Pfad``` in den Ordner mit den Dateien navigiert werden.
Nun müssen nacheinander folgende Befehle ausgeführt werden:

```kubectl apply -f mysql-secret.yaml```

```kubectl apply -f mysql-pv-pvc.yaml```

```kubectl apply -f mysql-statefulset.yaml```

```kubectl apply -f mysql-service.yaml```

```kubectl apply -f wordpress-pv-pvc.yaml```

```kubectl apply -f wordpress-deployment.yaml```

Jetzt sollte mit dem Befehl ```kubectl get svc wordpress-service``` nachgeschaut werden, was die "External-IP" ist. Bis diese erscheint könnten ein paar Minuten vergehen.
Sobald eine IP angezeigt wird, kann der Link http://"IhreExternalIP":30007 in einem Browserfenster eingegeben werden und es erscheint die Wordpress Seite.

## Beschreibungen der Dateien

Die YAML-Datei "mysql-secret.yaml" definiert ein Kubernetes Secret mit dem Namen "mysql-secret", dass das MySQL-Root-Passwort "password" enthält.

Die YAML-Datei "mysql-pv-pvc.yaml" definiert einen Persistent Volume mit dem Namen "mysql-pv", der 5 Gigabyte Speicherplatz auf einem Host-Pfad bereitstellt. Es enthält auch einen Persistent Volume Claim mit dem Namen "mysql-pvc", der 5 Gigabyte Speicherplatz anfordert und auf das PV mit dem Label "app: mysql" abzielt.

Die YAML-Datei "mysql-service.yaml" definiert einen Kubernetes Service mit dem Namen "mysql-service", der den TCP-Port 3306 für die MySQL-Datenbank öffnet. Der Service leitet den Datenverkehr an Pods weiter, die das Label "app: mysql" tragen.

Die YAML-Datei "mysql-statefulset.yaml" definiert ein Kubernetes StatefulSet mit dem Namen "mysql", das eine Replik eines MySQL-Containers erstellt. Das MySQL-Image "mysql:5.7" wird verwendet, und die Datenpersistenz wird durch einen Persistent Volume Claim für den Pfad "/var/lib/mysql" sichergestellt. 

Die YAML-Datei "wordpress-pv-pvc.yaml" definiert ein Persistent Volume mit dem Namen "wordpress-pv", das 10 Gigabyte Speicherplatz auf einem Host-Pfad bereitstellt. Es enthält auch einen Persistent Volume Claim mit dem Namen "wordpress-pvc", der 1 Gigabyte Speicherplatz anfordert und das PV mit dem Storage-Class-Namen "manual" verwendet.

Die YAML-Datei "wordpress-deployment.yaml" definiert ein Kubernetes Deployment, das zwei Replikate des WordPress-Containers erstellt. Der WordPress-Container verwendet das Image "wordpress:5.8.3-php7.4-apache" und ist mit einem Persistent Volume Claim für die Datenbindung konfiguriert. Ein Service mit dem Namen "wordpress-service" wird erstellt und als Load Balancer mit dem Port 80 konfiguriert, um auf den WordPress-Container zuzugreifen.

## Weitere Bilder:

Cluster Status mit der URL: https://portal.azure.com/#@fhwn.ac.at/resource/subscriptions/f27379d5-931b-49b4-a4a8-a7490d71fc75/resourceGroups/grasnick23/providers/Microsoft.ContainerService/managedClusters/grasnick23/overview
![cluster status neu erstellt](https://github.com/RatteF/Lab4/assets/83348757/8fc500e0-c5c9-47bc-a649-b0e232be7a45)
Laufendes Cluster
![laufendes kluster](https://github.com/RatteF/Lab4/assets/83348757/bcdbeafe-ac88-4373-a63a-143887fa3e4c)

