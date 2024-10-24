# Commande, Alias et config.
### A faire impérativement

Sur cette doc, vous trouverez des alias utile pour simplifier votre vie, de la config dans /etc/host pour eviter de connaitre les IPs, l'installation de commande, et surtout, comment configurer sa machine pour avoir accès au cluster kube.

## **Commande :
* **kubectl** pour gérer son cluster
* **helm** pour déployer des images / conteneurs /services etc...
* **k9s** pour gérer plus facilement son cluster, avec une "interface graphique"

### Kubectl   
```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

### helm
Nous utilisons des Heml charts pour déployer nos images.
* Windows


* Linux
```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

* MacOs
```bash
brew install helm
```

##### Ajouter dépôt de chats helm
Helm utilise des dépots pour stocker les charts. On vas utiliser le dépot officiel de helm.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

### k9s
```bash
wget https://github.com/derailed/k9s/releases/download/v0.32.5/k9s_linux_amd64.deb && apt install ./k9s_linux_amd64.deb && rm k9s_linux_amd64.deb
```

## **Alias
```bash
echo "alias k='kubectl'" >> ~/.zshrc
```

## **Hosts
* permet d'eviter de noter les adresses IP
* pour master
* pour worker 1
* pour worker 2
* pour Windows Server

(se mettre en root)
```bash
echo -e "192.168.0.68    e-corpwindows\n192.168.0.69    e-corpwindows\n192.168.0.70    e-corpmaster\n192.168.0.71    e-corpworker1\n192.168.0.72    e-corpworker2" >> /etc/hosts
```


## **Config

Créer le dossier .kube, dans son repertoire utilisateur, et lui attribuer des droits :
```bash
mkdir ~/.kube
cd ~/.kube
vim config
chmod 600 ~/.kube/config
```

mettre cette conf dans le fichier ~/.kube/config
```yaml
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJlVENDQVIrZ0F3SUJBZ0lCQURBS0JnZ3Foa2pPUFFRREFqQWtNU0l3SUFZRFZRUUREQmx5YTJVeUxYTmwKY25abGNpMWpZVUF4TnpJNU5UazVNamt6TUI0WERUSTBNVEF5TWpFeU1UUTFNMW9YRFRNME1UQXlNREV5TVRRMQpNMW93SkRFaU1DQUdBMVVFQXd3WmNtdGxNaTF6WlhKMlpYSXRZMkZBTVRjeU9UVTVPVEk1TXpCWk1CTUdCeXFHClNNNDlBZ0VHQ0NxR1NNNDlBd0VIQTBJQUJQTUxmbElPVDV1Ymd6OCtvRlBHNlBCb3lob2xNSGlYTGJPMlhBdzEKcDZleUMxNVlTUkRUQzR0MkwzQ1lQaUhhRFA5ZitWR1hOSG12L2F4NzlnbVhzc09qUWpCQU1BNEdBMVVkRHdFQgovd1FFQXdJQ3BEQVBCZ05WSFJNQkFmOEVCVEFEQVFIL01CMEdBMVVkRGdRV0JCUXZwVFNzdnlWQjFQQVBTT1lFCnJoZWl2Nk15N1RBS0JnZ3Foa2pPUFFRREFnTklBREJGQWlFQTMrNW9rV0J6ejBVUDlidjFmRVlZMW9rcit0VUMKWGJHZ3lxTWdTZENYTWh3Q0lHRlhUazNvNk1pUG8weW85M1RobDlRZ2ZNcFVYd0ErSkkrYzc3QjNHcVJhCi0tLS0tRU5EIENFUlRJRklDQVRFLS0tLS0K
    server: https://192.168.0.70:6443
  name: default
contexts:
- context:
    cluster: default
    user: default
  name: default
current-context: default
kind: Config
preferences: {}
users:
- name: default
  user:
    client-certificate-data: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUJrakNDQVRpZ0F3SUJBZ0lJWlVqQmtib3M5VE13Q2dZSUtvWkl6ajBFQXdJd0pERWlNQ0FHQTFVRUF3d1oKY210bE1pMWpiR2xsYm5RdFkyRkFNVGN5T1RVNU9USTVNekFlRncweU5ERXdNakl4TWpFME5UTmFGdzB5TlRFdwpNakl4TWpFME5UTmFNREF4RnpBVkJnTlZCQW9URG5ONWMzUmxiVHB0WVhOMFpYSnpNUlV3RXdZRFZRUURFd3h6CmVYTjBaVzA2WVdSdGFXNHdXVEFUQmdjcWhrak9QUUlCQmdncWhrak9QUU1CQndOQ0FBVGZZd3JzUmVMT0xIYVoKd2JGRC85YkVsaENFRWVMejQ5T0lRZWVsQ1lzNFNiNmR0Y2gyMkdBSXNXYURtaS9YYzJLNm1lM2dVT29UcTB3MQpYV01KQjJ6dm8wZ3dSakFPQmdOVkhROEJBZjhFQkFNQ0JhQXdFd1lEVlIwbEJBd3dDZ1lJS3dZQkJRVUhBd0l3Ckh3WURWUjBqQkJnd0ZvQVVyQUszTStaelJtVWFkRWFJTUMyZWZWYWJaNG93Q2dZSUtvWkl6ajBFQXdJRFNBQXcKUlFJaEFLV1JEN0VOZEptT1g1eVZLRHNvcDB2bFNGdVVFV2dRUXhTajgyaUsyT3V2QWlBU0dmemw3V05xRUVpKwpuNjZWNGZnVkZYdm5vZVhGQUl2MTF0MGhUWTFGNUE9PQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCi0tLS0tQkVHSU4gQ0VSVElGSUNBVEUtLS0tLQpNSUlCZURDQ0FSK2dBd0lCQWdJQkFEQUtCZ2dxaGtqT1BRUURBakFrTVNJd0lBWURWUVFEREJseWEyVXlMV05zCmFXVnVkQzFqWVVBeE56STVOVGs1TWprek1CNFhEVEkwTVRBeU1qRXlNVFExTTFvWERUTTBNVEF5TURFeU1UUTEKTTFvd0pERWlNQ0FHQTFVRUF3d1pjbXRsTWkxamJHbGxiblF0WTJGQU1UY3lPVFU1T1RJNU16QlpNQk1HQnlxRwpTTTQ5QWdFR0NDcUdTTTQ5QXdFSEEwSUFCTVYxc3d1V2hWbE45bjlEdnE3RUZsQlhicWpPL25BV1BFSkpkVmJUCmx3NU4yQjI0VzM0VTFKQW9oc2tOeEZuV3IvYnVCNEgxQS9Yd2tWTFd2VFhzNE5PalFqQkFNQTRHQTFVZER3RUIKL3dRRUF3SUNwREFQQmdOVkhSTUJBZjhFQlRBREFRSC9NQjBHQTFVZERnUVdCQlNzQXJjejVuTkdaUnAwUm9ndwpMWjU5VnB0bmlqQUtCZ2dxaGtqT1BRUURBZ05IQURCRUFpQXJLUTNwUFI2dDlRZzZLVUtGcEdRM0ZEeldQVmlsCnRZOWRMcUFmMGZiSzJBSWdia3o3VjRRMGM5Z09HeVlUSjNtWWQ3dUZFcEpORG00d3VzTUZ0SDRFaE5BPQotLS0tLUVORCBDRVJUSUZJQ0FURS0tLS0tCg==
    client-key-data: LS0tLS1CRUdJTiBFQyBQUklWQVRFIEtFWS0tLS0tCk1IY0NBUUVFSUdxNytPY25DUC9kTDJnckx1MUJiRW1vZm8yYWJtb1lrSWozRGFMSzc2YnlvQW9HQ0NxR1NNNDkKQXdFSG9VUURRZ0FFMzJNSzdFWGl6aXgybWNHeFEvL1d4SllRaEJIaTgrUFRpRUhucFFtTE9FbStuYlhJZHRoZwpDTEZtZzVvdjEzTml1cG50NEZEcUU2dE1OVjFqQ1Fkczd3PT0KLS0tLS1FTkQgRUMgUFJJVkFURSBLRVktLS0tLQo=
```

Tester la connexion

```bash
kubectl get nodes
```
cela devrais renvoyer les nodes du cluster.
Si le cluster n'est pas UP, c'est normal que la commande marche pas.

## Mettre sa clef ssh sur le Master et Worker node
Pour éviter de mettre le mot de passe..
```
scp ~/.ssh/id_rsa.pub e-corp@e-corpmaster:~/id_rsa.pub.tmp
ssh e-corp@e-corpmaster 'cat ~/id_rsa.pub.tmp >> ~/.ssh/authorized_keys && rm ~/id_rsa.pub.tmp && chmod 600 ~/.ssh/authorized_keys'
```

