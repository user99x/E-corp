# Récapitulatif de la configuration des comptes utilisateurs et des accès dans Active Directory

## 1. Création des comptes utilisateurs dans Active Directory

### Étapes :
1. **Ouvrir Active Directory Users and Computers (ADUC)** sur le contrôleur de domaine.
2. Allez dans l'**OU** appropriée (ex : **Users** ou créer des OUs spécifiques pour Emmanuel et Max).
3. Clic droit sur l'OU et sélectionner **New** > **User**.
4. Remplir les informations pour **Emmanuel (CDI)** et **Max (Alternant)** :
   - Nom, prénom et nom d'utilisateur
   - Mot de passe (ne pas cocher "User must change password at next logon" si vous ne voulez pas que l'utilisateur change son mot de passe au premier login).
5. Créer les **groupes de sécurité** :
   - **CDI_Groupe** pour Emmanuel
   - **Alternant_Groupe** pour Max

## 2. Création des groupes de sécurité et affectation des utilisateurs

### Étapes :
1. Créer les groupes **CDI_Groupe** et **Alternant_Groupe** dans **Active Directory** :
   - Clic droit sur **Groups** > **New** > **Group**.
   - Assurez-vous que le type de groupe est **Sécurité**.
2. **Ajouter Emmanuel** au groupe **CDI_Groupe** et **Max** au groupe **Alternant_Groupe**.

## 3. Configuration des permissions NTFS pour les dossiers partagés

### Étapes :
1. Créez les **dossiers partagés** sur les serveurs ou ordinateurs où les ressources seront stockées.
2. Allez dans les **propriétés** des dossiers, puis dans l'onglet **Sécurité**.
3. Ajoutez les groupes **CDI_Groupe** et **Alternant_Groupe** :
   - **CDI_Groupe** : permissions complètes ou spécifiques sur le dossier réservé aux CDI (ex : **CDI_Resources**).
   - **Alternant_Groupe** : permissions restreintes (ex : lecture seule) sur le dossier réservé aux alternants (ex : **Alternant_Resources**).

## 4. Configuration des stratégies de groupe (GPO) pour personnaliser les paramètres

### Étapes :
1. Créer des **GPO** spécifiques pour **CDI_Groupe** et **Alternant_Groupe** :
   - Exemple : Mapper des lecteurs réseau, définir des restrictions d'applications ou des paramètres de bureau.
2. **Appliquer les GPO** sur les **OUs** où se trouvent les comptes d'Emmanuel et Max.
3. Pour appliquer immédiatement les GPO :
   - Utilisez la commande `gpupdate /force` sur les PCs de Emmanuel et Max.
   - Utilisez `rsop.msc` pour vérifier les GPO appliquées.

## 5. Joindre les PCs au domaine Active Directory

### Étapes :
1. **Joindre les PCs** (Emmanuel et Max) au domaine Active Directory :
   - Ouvrir **Paramètres système** > **Système** > **Informations système** > **Paramètres de domaine**.
   - Entrer les informations du domaine et redémarrer le PC.
2. Vérifiez que les PCs sont bien ajoutés au domaine via la commande `dsget computer`.

## 6. Connexion avec les comptes utilisateurs du domaine

### Étapes :
1. **Se connecter au PC avec les comptes du domaine** :
   - Sur l'écran de connexion, entrer **Emmanuel** ou **Max** suivi du domaine, ex : `exemple\Emmanuel` ou `exemple\Max`.
2. Vérifier que l'utilisateur peut se connecter avec ses **identifiants de domaine**.

## 7. Configurer les profils utilisateurs locaux sur les PCs

### Étapes :
1. Les **dossiers de profil utilisateur** pour **Emmanuel** et **Max** seront créés localement sur chaque PC sous `C:\Users\Emmanuel` et `C:\Users\Max`.
2. **Vérifiez les permissions NTFS** sur les dossiers locaux pour protéger l'accès aux fichiers :
   - **Emmanuel** doit avoir un accès total à son propre dossier.
   - **Max** doit avoir un accès limité à son propre dossier.

## 8. Vérification des accès et des permissions

### Étapes :
1. **Tester les connexions** sur chaque PC en vous connectant avec les comptes **Emmanuel** et **Max**.
2. Vérifier que **Emmanuel** a accès aux ressources de **CDI** et **Max** seulement aux ressources de **Alternant**.
3. Utiliser **l'explorateur de fichiers** pour tester les accès aux dossiers partagés et mappés (ex : **CDI_Resources** et **Alternant_Resources**).

## 9. Tests et validation

### Étapes :
1. Connectez-vous avec le compte **Emmanuel** et vérifiez l'accès aux dossiers spécifiques aux CDI.
2. Connectez-vous avec le compte **Max** et vérifiez l'accès aux dossiers spécifiques aux alternants.
3. Vérifiez que les **permissions NTFS** sont respectées et que les **stratégies de groupe** sont appliquées comme prévu.

---

## Résumé des éléments à vérifier :

1. **Comptes utilisateurs** dans Active Directory : Emmanuel et Max.
2. **Groupes de sécurité** : CDI_Groupe et Alternant_Groupe.
3. **Permissions NTFS** sur les dossiers partagés et locaux.
4. **Stratégies de groupe (GPO)** appliquées pour personnaliser les environnements de travail.
5. **Joindre les PCs** au domaine et connexion avec les comptes utilisateurs.
6. **Tests des accès** pour s'assurer que les permissions sont respectées.
