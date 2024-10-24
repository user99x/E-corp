# 🖥️ Installation de l'Active Directory sur Windows Server 2022

## Introduction

L'un des produits les plus emblématiques de **Windows Server** dans les environnements professionnels est l'**Active Directory (AD)**. Cette solution d'authentification unique (Single Sign-On) permet une gestion simple et centralisée des utilisateurs, des ordinateurs et des ressources sur le réseau. Ce guide vous accompagne à travers les étapes nécessaires pour installer les services de domaine **Active Directory (AD DS)** sur un **Windows Server 2022** fraîchement installé.

---

## 1️⃣ Ajouter les rôles et fonctionnalités (AD DS)

1. **Ouvrir le Gestionnaire de Serveur**  
    Cliquez sur **Gérer** puis sélectionnez **Ajouter des rôles et des fonctionnalités**.
    
    ![[../image/Pasted image 20241024125042.png]]
    
2. **L'Assistant d'ajout de rôles et de fonctionnalités** s'ouvre. Cliquez sur **Suivant** pour continuer.
    
    ![[Pasted image 20241024125220.png]]
    
3. Dans la section **Type d'installation**, laissez **Installation basée sur un rôle ou une fonctionnalité** sélectionné et cliquez sur **Suivant**.
    
    ![[Pasted image 20241024125242.png]]
    
4. **Sélectionner le serveur de destination**  
    Choisissez le serveur sur lequel vous voulez installer **AD DS**. Ici, nous sélectionnons le serveur local: **Windows Server 2022 Standard Evaluation**.
    

---

## 2️⃣ Configurer le rôle AD DS

1. **Sélectionner le rôle AD DS**  
    Cochez l'option **Services AD DS** (Services de domaine Active Directory) et cliquez sur **Ajouter des fonctionnalités** lorsque la fenêtre apparaît.
    
2. **Vérification des services AD DS**  
    Vous devriez voir que le rôle **Services AD DS** est bien sélectionné. Cliquez ensuite sur **Suivant**.
    
3. **Fonctionnalités supplémentaires**  
    Sur la page **Sélectionner les fonctionnalités**, vous pouvez ajouter des options supplémentaires si nécessaire. Dans ce guide, nous choisissons une installation standard sans fonctionnalités supplémentaires. Cliquez simplement sur **Suivant**.
    
4. **Confirmation de l'installation**  
    Revoyez les éléments sélectionnés. Si tout vous semble correct, cochez la case permettant de redémarrer le serveur automatiquement si nécessaire, puis cliquez sur **Installer**.
    
5. **Installation en cours**  
    Une fois l'installation terminée, cliquez sur **Fermer**.
    

---

## 3️⃣ Promouvoir le serveur en contrôleur de domaine

1. **Accéder à la notification**  
    Une fois AD DS installé, retournez dans le **Gestionnaire de serveur**. Une notification jaune apparaîtra à côté de l'onglet **Gérer**. Cliquez dessus et choisissez **Promouvoir ce serveur en contrôleur de domaine**.
    
2. **Assistant de configuration**  
    L'**Assistant de configuration des services de domaine Active Directory** s'ouvre. Vous allez ici créer une nouvelle forêt. Saisissez le **Nom de domaine racine** de votre organisation, puis cliquez sur **Suivant**.
    
3. **Options du contrôleur de domaine**  
    Laissez les paramètres par défaut et entrez votre mot de passe de récupération. Cliquez sur **Suivant**.
    
4. **Option DNS**  
    Une erreur liée à la délégation DNS peut apparaître : _"Une délégation pour ce serveur DNS ne peut pas être créée car le serveur de noms de zone parente autoritaire ne peut pas être trouvé"_. Ignorez cette erreur en cliquant simplement sur **Suivant**.
    

---

## 4️⃣ Configurations supplémentaires

1. **Nom de domaine NetBIOS**  
    Laissez le nom par défaut ou modifiez-le si nécessaire (limité à 15 caractères). Cliquez sur **Suivant**.
    
2. **Chemins de stockage par défaut**  
    Laissez les chemins de stockage des fichiers AD par défaut, sauf si vous avez des besoins spécifiques. Cliquez sur **Suivant**.
    
3. **Résumé des paramètres**  
    Vérifiez les choix que vous avez effectués. Si tout vous convient, cliquez sur **Suivant**.
    
4. **Validation des prérequis**  
    Le serveur validera les prérequis. Si des erreurs surviennent, corrigez-les avant de continuer. Sinon, cliquez sur **Installer**.
    
5. **Redémarrage**  
    Une fois l'installation terminée, cliquez sur **Fermer**. Le serveur redémarrera automatiquement.
    

---

## 🎉 Connexion au domaine

Après le redémarrage du serveur, vous pouvez maintenant vous connecter au domaine avec les identifiants que vous avez définis lors de la configuration. Votre **Windows Server 2022** est maintenant configuré en tant que **Contrôleur de domaine** avec **Active Directory** !
