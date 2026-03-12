
## Doc 5

```markdown
# Mission 4 : Recherche et mise en place d'un outil de gestion d'incident

---

**MANCEAU RAHMY — Léandre Arthur**

| Activités Professionnelles Situation professionnelle | Mille nuits | Gestion du parc informatique | SP 2 |
| :--- | :---: | :--- | :---: |

## Installation de GLPI sur Debian 12

### Prérequis

- Système Debian 12 à jour
- Serveur web Apache ou Nginx
- PHP (version compatible avec GLPI)
- Base de données MySQL/MariaDB

### Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install apache2 mariadb-server php php-mysql php-curl php-xml php-gd php-mbstring wget

cd /tmp
wget -O glpi.tgz https://github.com/glpi-project/glpi/releases/latest/download/glpi.tgz

sudo mysql -u root -p
CREATE DATABASE glpidb;
CREATE USER 'glpiuser'@'localhost' IDENTIFIED BY 'motdepasse';
GRANT ALL PRIVILEGES ON glpidb.* TO 'glpiuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
