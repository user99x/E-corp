# Documentation de Maintenance pour Windows Server 2019 sur VirtualBox

## Table des Matières
1. [Introduction](#introduction)
2. [Prérequis](#prérequis)
3. [Accès à la VM](#accès-à-la-vm)
4. [Tâches de Maintenance Hebdomadaires](#tâches-de-maintenance-hebdomadaires)
5. [Tâches de Maintenance Mensuelles](#tâches-de-maintenance-mensuelles)
6. [Résolution des Problèmes Communs](#résolution-des-problèmes-communs)
7. [Sauvegarde et Restauration](#sauvegarde-et-restauration)
8. [Mises à Jour et Patches](#mises-à-jour-et-patches)
9. [Arrêt et Redémarrage de la VM](#arrêt-et-redémarrage-de-la-vm)

---

## Introduction
Ce document décrit les tâches de maintenance essentielles pour garantir la performance et la sécurité d'un serveur Windows Server 2019 hébergé sur une machine virtuelle (VM) via VirtualBox.

---

## Prérequis
- VirtualBox installé avec une version compatible.
- Accès administratif à la VM et à VirtualBox.
- Espace disque suffisant sur le système hôte pour les sauvegardes et snapshots.
- Connaissance de base de l'environnement Windows Server.

---

## Accès à la VM
### Depuis VirtualBox :
1. Lancez VirtualBox.
2. Sélectionnez la VM contenant Windows Server 2019.
3. Cliquez sur **Démarrer** pour initialiser la VM.
4. Connectez-vous avec un compte administrateur.

### Depuis le Réseau (RDP) :
1. Assurez-vous que le RDP est activé sur le serveur.
2. Utilisez un client RDP (ex. : `mstsc`) pour accéder au serveur.
3. Entrez l'adresse IP de la VM et connectez-vous avec des identifiants valides.

---

## Tâches de Maintenance Hebdomadaires
1. **Vérification des ressources système :**
   - Ouvrez le **Gestionnaire des tâches** ou utilisez **PerfMon** pour surveiller l'utilisation CPU, RAM et disque.
   - Identifiez les processus gourmands.

2. **Vérification des journaux d'événements :**
   - Ouvrez l'outil **Observateur d'événements**.
   - Analysez les sections **Système** et **Sécurité** pour détecter des erreurs ou des avertissements.

3. **Gestion des utilisateurs et droits :**
   - Révisez les comptes d'utilisateurs et supprimez ceux inutilisés.
   - Vérifiez les groupes d’administration.

4. **Sauvegarde des données critiques :**
   - Assurez-vous que les sauvegardes planifiées ont été effectuées correctement.
   - Testez la récupération à partir d'une sauvegarde.

---

## Tâches de Maintenance Mensuelles
1. **Mises à jour système :**
   - Exécutez **Windows Update** pour télécharger et installer les correctifs de sécurité.
   - Redémarrez si nécessaire.

2. **Défragmentation et optimisation du disque :**
   - Ouvrez **Optimiser les lecteurs** pour vérifier si la défragmentation est nécessaire.

3. **Snapshot de la VM :**
   - Dans VirtualBox, créez un snapshot avant toute modification majeure :
     - Menu **Machine** > **Prendre un instantané**.

4. **Vérification de la sécurité réseau :**
   - Analysez les règles de pare-feu configurées via **Windows Defender Firewall**.
   - Exécutez un scan antivirus/malware.

---

## Résolution des Problèmes Communs
### La VM ne démarre pas :
- Assurez-vous que le système hôte dispose de suffisamment de mémoire et d'espace disque.
- Vérifiez la configuration des **paramètres système** dans VirtualBox.

### Problèmes réseau :
- Confirmez que l'adaptateur réseau de la VM est configuré correctement (NAT, Pont, etc.).
- Redémarrez le service réseau avec :  
  ```bash
  net stop dhcp && net start dhcp
  ```

### Performances lentes :
- Vérifiez si une fragmentation excessive est en cours.
- Augmentez la RAM ou les processeurs attribués à la VM dans VirtualBox.

---

## Sauvegarde et Restauration
### Sauvegarde :
1. Créez un snapshot de la VM dans VirtualBox.
2. Exportez la VM via **Fichier > Exporter vers un fichier OVF**.

### Restauration :
1. Importez un fichier OVF via **Fichier > Importer un appareil virtuel**.
2. Restaurez les données à partir des sauvegardes.

---

## Mises à Jour et Patches
- Lancez **Windows Server Update Services** (WSUS) ou Windows Update.
- Configurez les mises à jour automatiques :
  - Ouvrez **Stratégie de groupe** avec `gpedit.msc`.
  - Accédez à **Configuration ordinateur > Modèles d'administration > Composants Windows > Windows Update**.

---

## Arrêt et Redémarrage de la VM
### Depuis VirtualBox :
1. Cliquez sur **Machine > Fermer > Envoyer l'ordre d'arrêt**.
2. Assurez-vous que la VM est éteinte avant d'effectuer des modifications.

### Depuis Windows Server :
1. Ouvrez une session administrateur.
2. Exécutez la commande :  
   ```bash
   shutdown /s /t 0
   ```

---

## Notes
- Tenez un journal des tâches de maintenance effectuées.
- Planifiez des audits de sécurité trimestriels pour renforcer la protection.
