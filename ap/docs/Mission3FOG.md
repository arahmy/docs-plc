# Mission 3 — Recherche et mise en place d’un outil de déploiement des postes

**Nom :** Léandre MANCEAU  

---

# 1. Objectif de la mission

L’objectif de cette mission est de rechercher un **outil permettant de déployer des postes informatiques rapidement** sur un réseau.  
Ces outils permettent notamment de :

- installer automatiquement un système d’exploitation
- cloner un poste vers plusieurs machines
- automatiser la configuration des ordinateurs

Trois solutions ont été étudiées :

- **FOG**
- **Clonezilla**
- **Microsoft Deployment Toolkit (MDT)**

---

# 2. Comparaison des solutions

| Outil | Fonctionnalités | Points forts | Points faibles | Coût |
|------|------|------|------|------|
| **FOG** | Déploiement d’images système via le réseau | - Gratuit <br> - Interface web simple <br> - Compatible multi-OS | - Configuration initiale parfois complexe <br> - Gestion des pilotes limitée <br> - Nécessite un serveur Linux | Gratuit (Open Source) |
| **Clonezilla** | Clonage de disque et création d’images | - Simple et puissant <br> - Open Source <br> - Fonctionne sans installation (Live USB) | - Peu d’automatisation <br> - Interface limitée | Gratuit (Open Source) |
| **Microsoft Deployment Toolkit (MDT)** | Déploiement automatisé de Windows | - Très puissant pour les environnements Windows <br> - Intégration avec Active Directory | - Configuration complexe <br> - Windows uniquement <br> - Nécessite souvent Windows Server | Gratuit mais nécessite des licences Windows Server |

---

# 3. Choix de la solution

La solution **FOG** a été retenue pour cette mission car :

- elle est **open source**
- elle permet le **déploiement réseau automatisé**
- elle possède une **interface web de gestion**
- elle peut gérer **plusieurs systèmes d’exploitation**

---

# 4. Mise en place de FOG

## 4.1 Création de la machine virtuelle

La machine virtuelle est créée sur l’infrastructure **Nutanix** avec les paramètres suivants :

- **Système d’exploitation :** Debian 12  
- **Adresse IP :** `172.16.56.10`  
- **Rôle :** serveur de déploiement FOG

L’adresse IP est configurée afin de correspondre au réseau du groupe.

---

## 4.2 Installation des dépendances

Ces commandes installent Git, téléchargent le FOG Project depuis GitHub, passent sur la version stable du projet, puis lancent le script d’installation installfog.sh pour installer automatiquement FOG sur notre serveur. 

La première étape consiste à installer **Git**, nécessaire pour récupérer le projet FOG depuis GitHub.

```bash
sudo -i
apt-get -y install git 
```
```bash
sudo -i
cd /root
git clone https://github.com/FOGProject/fogproject.git
cd fogproject
```
```bash
cd /root/fogproject
git fetch --all
```
```bash
git checkout stable
```
```bash
  sudo -i
  cd /root/fogproject/bin
  ./installfog.sh
```