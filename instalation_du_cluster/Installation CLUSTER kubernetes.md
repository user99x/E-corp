prérequis : 
* Se connecter au réseau sur le switch
* curl installé
* avoir les droits root
* avoir fait toute sa config sur son Localhost ([[Configuration de sa machine]])
* Pouvoir se connecter au Master node et Worker node


# Installation MASTER NODE
### SSH :
Se connecter en ssh, pour pouvoir copier coller (ça marche pas sur proxmox)
```bash
ssh e-corp@ecorpmaster
#se mettre en root
sudo su
```

## Installer RKE2
RKE2 sert a installer le cluster kube.
```bash
curl -sfL https://get.rke2.io | sh -
```

### Installer containerd 
```bash
apt install containerd
```
## Configurer RKE2 pour le master node

Créer un fichier comme ceci :
```bash
mkdir -p /etc/rancher/rke2
vim /etc/rancher/rke2/config.yaml
```

et mettre cette config yaml dedans :

```yaml
write-kubeconfig-mode: "0644"
tls-san:
  - "<IP_PUB_MASTERNODE>"
container-runtime-endpoint: unix:///run/containerd/containerd.sock
```

## Demarer et activer service rke2 en mode serveur

```bash
systemctl enable rke2-server
systemctl start rke2-server
```
Cela peux prendre entre 30 sec et 2 min.
verifier le status : 
```bash
journalctl -u rke2-server -f
```

## Obtenir le token pour acceder au worker node

```bash
cat /var/lib/rancher/rke2/server/node-token
```
Important : garder le jeton est nécessaire pour les étape d'après. Je le conseille de le noter quelque part temporairement.

## Configurer kubectl sur le master node
kubectl est la commande pour interagir avec le cluster.
```bash
export KUBECONFIG=/etc/rancher/rke2/rke2.yaml
export PATH=$PATH:/var/lib/rancher/rke2/bin
```

### Conseil:
ajouter ces ligne dans le .bashrc, pour l'avoir automatiquement après chaque connexion ssh.
```bash
vim ~/.bashrc
```

## Vérifier le fonctionement de kubectl
```bash
k get nodes
```

cette commande devrais renvoyer quelques chose comme ceci :
![[Pasted image 20241022095734.png]]
et sert a connaitre les nodes actifs sur un cluster.


# Installation de WORKER NODE

### SSH :
Se connecter en ssh, pour pouvoir copier coller (ça marche pas sur proxmox)
```bash
ssh e-corp@ecorpmaster
#se mettre en root
sudo su
```

## Installer RKE2 sur worker node
```bash
curl -sfL https://get.rke2.io | sh -
```

## Créer fichier de conf:
```bash
mkdir -p /etc/rancher/rke2
vim /etc/rancher/rke2/config.yaml
```
### Mettre cette conf :
reprendre le token sauvegardé précédemment :
```yaml
server: https://<IP_PUB_MASTERNODE>:9345
token: "<TOKEN>"
```


## Demarrer et activer rke2 en mode worker
```bash
systemctl enable rke2-agent
systemctl start rke2-agent
```
Entre 1 min et 3 min pour se lancer

### vérifier le status
```bash
journalctl -u rke2-agent -f
systemclt status rke2-agent
```

