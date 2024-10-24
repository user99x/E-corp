
![Logo Proxmox](https://upload.wikimedia.org/wikipedia/commons/9/92/Logo_Proxmox.svg)

# Installation de Proxmox sur un PC avec IP 192.168.1.69

## Prérequis
- Un PC compatible pour installer Proxmox.
- Une clé USB bootable avec Proxmox VE.
- Accès à un réseau local pour la configuration IP.
- Connexion internet stable.

## Étapes d'installation

### 1. Préparer la clé USB d'installation
- Téléchargez l'ISO de Proxmox VE à partir du site officiel : [Proxmox VE ISO](https://www.proxmox.com/en/downloads).
- Utilisez un logiciel tel que [Rufus](https://rufus.ie) ou [Balena Etcher](https://www.balena.io/etcher/) pour créer une clé USB bootable avec l'ISO téléchargé.

### 2. Configurer le BIOS du PC
- Redémarrez le PC et accédez au BIOS en appuyant sur la touche `DEL` ou `F2` (selon le fabricant).
- Modifiez l'ordre de démarrage pour que la clé USB soit le premier périphérique de boot.
- Sauvegardez et quittez le BIOS.

### 3. Démarrer l'installation de Proxmox
- Démarrez à partir de la clé USB contenant Proxmox.
- Sélectionnez l'option **Install Proxmox VE**.

### 4. Configurer les paramètres d'installation
- Acceptez les termes de la licence Proxmox.
- Sélectionnez le disque sur lequel Proxmox sera installé.
- Configurez le fuseau horaire, le clavier, et créez un mot de passe pour l'utilisateur root.
- **Paramètres réseau :**
  - `Hostname` : proxmox.local
  - `IP` : 192.168.1.69/24
  - `Gateway` : 192.168.1.1 (ou selon votre routeur)
  - `DNS` : 8.8.8.8 (ou selon vos préférences)

### 5. Finaliser l'installation
- Cliquez sur **Installer** et attendez la fin du processus.
- Une fois terminé, retirez la clé USB et redémarrez le PC.

### 6. Accéder à l'interface Proxmox
- Depuis un autre ordinateur sur le même réseau, ouvrez un navigateur et entrez l'adresse suivante : https://192.168.0.69:8006
- - Ignorer l'avertissement de certificat et connectez-vous avec les informations root créées durant l'installation.

### 7. Mise à jour de Proxmox
- Après la connexion, ouvrez une console sur Proxmox et exécutez les commandes suivantes pour mettre à jour le système :
```
apt update
apt full-upgrade
```

Ce fichier fournit les étapes détaillées pour une installation complète de Proxmox avec une IP spécifique.