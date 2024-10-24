## Exemple création d'application avec helm chart 

prenon l'exemple de apache

### Rechercher la chart apache
```bash
helm repo update
helm search repo apache
```

bitnami/apache est ce qu'il faut prendre.

### Création du namespace pour apache
```bash
kubectl create namespace apache-web
```

### Installer apache dans ce namespace
```bash
helm install my-apache bitnami/apache --namespace apache-web
```
Cette comandde permet d'installer tous les éléments necessaire au bon foncitonnement du pod.
### Vérifier l'instalation du pod :
```bash
kubectl get pods
```


Vérifier si le pod expose bien.
Sur k9s, aller dans les services.    
```
:svc
```
chercher le pod apache,
faire shift f, et faire terminer.
Un port forward sur le cluster kube est lancé.
Maintenant, lancer un tunnel ssh , de sa machine vers le masternode.
```bash
ssh -L 8080:localhost:8080 e-corp@e-corpmaster
```