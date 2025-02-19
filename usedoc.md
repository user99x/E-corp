# Utiliser et contribuer à la DOC

## 1. Introduction
MkDocs est un générateur de documentation statique simple et puissant écrit en Python. Cette documentation vous guidera à travers l'installation de MkDocs sur Linux et Windows, en partant de zéro.

---

## 2. Prérequis
Avant d'installer MkDocs, assurez-vous d'avoir installé **Git**, **Python** et **pip** (le gestionnaire de paquets Python).

### Installation de Git

#### Sous Linux
1. **Mettre à jour le système** :
   ```sh
   sudo apt update && sudo apt upgrade -y
   ```
2. **Installer Git** :
   ```sh
   sudo apt install git -y
   ```
3. **Vérifier l'installation** :
   ```sh
   git --version
   ```

#### Sous Windows
1. **Télécharger Git** :
   - Rendez-vous sur : [https://git-scm.com/downloads](https://git-scm.com/downloads)
   - Téléchargez et installez la version correspondant à votre système.
   - Lors de l'installation, sélectionnez tout par défaut
2. **Vérifier l'installation** :
   - Ouvrez une invite de commande et tapez :
     ```sh
     git --version
     ```


## 3. Configurer git
1. **Configurer son email**
     ```sh
     git config --global.email "email.used@for.github"
     git config --global.user "githubuser"
     ```

### Vérifier si Python est déjà installé
Exécutez la commande suivante dans un terminal (Linux) ou l'invite de commande (Windows) :
```sh
python --version
```
Ou :
```sh
python3 --version
```
Si Python n'est pas installé, suivez les étapes ci-dessous.

---

## 4. Installation de Python et pip

### 4.1 Sous Linux
1. **Mettre à jour le système** :
   ```sh
   sudo apt update && sudo apt upgrade -y
   ```
2. **Installer Python et pip** :
   ```sh
   sudo apt install python3 python3-pip -y
   ```
3. **Vérifier l'installation** :
   ```sh
   python3 --version
   pip3 --version
   ```

### 4.2 Sous Windows
1. **Télécharger Python** :
   - Rendez-vous sur le site officiel : [https://www.python.org/downloads/](https://www.python.org/downloads/)
   - Téléchargez et installez la dernière version de Python.
   - Lors de l'installation, **cochez la case "Add Python to PATH"**.
2. **Vérifier l'installation** :
   - Ouvrez l'invite de commande et tapez :
     ```sh
     python --version
     pip --version
     ```
3. **Mettre à jour pip**
   - Lancer l'invite de commande et tapez:
     ```sh
     python -m pip install --upgrade pip
     ```

---

## 5. Installation de MkDocs

### 5.1 Sous Linux
1. **Installer MkDocs avec pip** :
   ```sh
   pip3 install mkdocs
   ```
2. **Vérifier l'installation** :
   ```sh
   mkdocs --version
   ```

### 5.2 Sous Windows
1. **Installer MkDocs avec pip** :
   ```sh
   pip install mkdocs
   ```
2. **Vérifier l'installation** :
   ```sh
   mkdocs --version
   ```

---

## 6. Utilisation de Git

### Initialiser le projet et le cloner
1. **Ajouter le dépôt distant et le cloner** :
   ```sh
   # sur github
   git clone https://github.com/CiscoDerm/E-Corp.git
   # sur notre infra
   git clone https://gitlab.ecorp.ad/root/documentation.git
   ```

### Contribuer à notre doc
1. **Créer une nouvelle branche** :
   ```sh
   git checkout -b feat/ma-branche
   ```
2. **Après avoir fait des modifications et les avoir validé (étape 6)**  les ajouter et commit :
   ```sh
   git add .
   git commit -m "feat: Ajout de l'ad"
   ```
3. **Pousser les modifications sur la branche distante** :
   ```sh
   git push origin feat/ma-branche
   ```
4. **Créer une merge request (Pull Request)** :
   - Aller sur GitHub/GitLab et ouvrir une Merge Request (Pull Request) vers la branche `main`.
   - Attendre la validation avant de fusionner.

---

## 7. Test rapide de MkDocs
1. **Aller dans la racine du projet** :
   ```sh
   cd E-corp
   ```
2. **Lancer le serveur local de documentation** :
   ```sh
   mkdocs serve
   ```
4. **Ouvrir dans un navigateur** :
   - Allez sur : [http://127.0.0.1:8000](http://localhost:8000)

---

## 8. Conclusion
Vous avez maintenant MkDocs installé et prêt à l'emploi sur Linux et Windows ! Vous savez également comment utiliser Git pour contribuer à un projet et gérer vos modifications efficacement. 🚀

