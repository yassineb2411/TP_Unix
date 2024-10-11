
# Rapport de TP : Installation et Configuration de Debian

## 1. Installation de Debian
L'installation de Debian a été réalisée à l'aide d'une image ISO (mini.iso). Les étapes principales comprenaient :

- **Choix de la langue et du clavier** : Sélection des paramètres régionaux.
- **Partitionnement** : Création manuelle de partitions pour `/`, `/tmp`, `/var/log` et `swap`. 
  - Difficultés rencontrées lors de la configuration des points de montage et de la taille des partitions.
- **Installation des paquets de base** : Cela a pris un certain temps et a nécessité la sélection du noyau approprié.
- **Installation de GRUB** : Configuration du chargeur de démarrage.

## 2. Post-Installation

### 2.1 Configuration de SSH
- Connexion en tant que `root` à la machine.
- Installation de SSH avec `apt search` et `apt install`.
- Modification du fichier de configuration `sshd_config` pour permettre les connexions root avec mot de passe.
  ```bash
  PermitRootLogin yes
  PasswordAuthentication yes
  ```

### 2.2 Connexion
- Connexion à la machine virtuelle depuis la machine hôte pour faciliter les opérations de copy-paste.

### 2.3 Nombre de paquets
- Vérification du nombre de paquets installés avec la commande :
  ```bash
  dpkg -l | wc -l
  ```
- Une installation légère devrait avoir environ 320 paquets. Résultat obtenu : **352 paquets**.

### 2.4 Utilisation de l'espace
- Vérification de l'utilisation de l'espace de la partition racine avec la commande :
  ```bash
  df -h
  ```
- La racine `/` doit représenter moins de 1 Go d'espace utilisé Résultat obtenu : **956Mo**.

### 2.5 Explications des commandes
- **Locales** : `echo $LANG` pour vérifier la langue.
- **Nom de la machine** : `hostname` pour afficher le nom de la machine.
- **Domaine** : Utiliser `hostname -d` pour afficher le domaine.

- **Vérification des dépôts** : 
  ```bash
  cat /etc/apt/sources.list | grep -v -E '^#|^$'
  ```
  La commande entière sert à afficher uniquement les lignes actives (non commentées et non vides) du fichier `sources.list`. Cela permet de voir rapidement les dépôts de paquets qui sont effectivement utilisés par le système pour l'installation et les mises à jour des logiciels.

- **Passwd/Shadow** : 
  ```bash
  cat /etc/shadow | grep -vE ':\*:|:!\*:'
  ```
  La commande entière sert à afficher uniquement les comptes utilisateurs qui ont un mot de passe valide (c'est-à-dire qui ne sont ni sans mot de passe ni désactivés) dans le fichier `/etc/shadow`. Cela permet d'obtenir une liste des utilisateurs actifs avec des mots de passe configurés sur le système.
  
- **Comptes utilisateurs** : 
  ```bash
  cat /etc/passwd | grep -vE 'nologin|sync'
  ```
  La commande entière sert à afficher uniquement les comptes utilisateurs qui ont un shell valide (c'est-à-dire qui ne sont pas configurés pour `nologin` ou `sync`) dans le fichier `/etc/passwd`. Cela permet d'obtenir une liste des utilisateurs actifs pouvant se connecter au système.

- **Explications des retours** : 
  - `fdisk -l` : Liste des partitions et de leur type.
  - `fdisk -x` : Cette commande liste toutes les partitions des disques connectés, ce qui est très utile pour obtenir un aperçu de la configuration du disque.
  - `df -h` : Affiche l'utilisation de l'espace sur le disque.

## 3. Aller plus loin

### 3.1 Installation automatique
- **Preseed** : Utilisé pour automatiser l'installation de Debian sans intervention manuelle.

### 3.2 Mode Rescue
- **Changement de mot de passe root** :  Le mode rescue est un outil précieux pour les administrateurs système, permettant de résoudre des problèmes sans avoir besoin de réinstaller le système d'exploitation.

### 3.3 Redimensionnement de la partition
- **Redimensionnement de la partition racine** : Utilisation d'un live CD/USB avec GParted pour modifier la taille de la partition sans réinstallation.


- **Sauvegardez vos données importantes**.
- **Démarrez avec un Live CD/USB** de Linux.
- **Ouvrez GParted** :
   - Sélectionnez le disque.
   - Redimensionnez la partition racine (`/`).
- **Redémarrez votre système**.
- **Vérifiez avec `df -h`** que le redimensionnement est réussi. 

**Remarque :** Assurez-vous d'avoir de l'espace libre avant d'agrandir ou de réduire la partition.



---



