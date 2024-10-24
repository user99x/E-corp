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


##### Copier la conf rke2 sur sa machine.
```bash
scp e-corp@e-corpmaster:/etc/rancher/rke2/rke2.yaml ~/.kube/config
```

Tester la connexion

```bash
k get nodes
```
cela devrais renvoyer les nodes du cluster.
Si le cluster n'est pas UP, c'est normal que la commande marche pas.

## Mettre sa clef ssh sur le Master et Worker node
Pour éviter de mettre le mot de passe..
```
scp ~/.ssh/id_rsa.pub e-corp@e-corpmaster:~/id_rsa.pub.tmp
ssh e-corp@e-corpmaster 'cat ~/id_rsa.pub.tmp >> ~/.ssh/authorized_keys && rm ~/id_rsa.pub.tmp && chmod 600 ~/.ssh/authorized_keys'
```

