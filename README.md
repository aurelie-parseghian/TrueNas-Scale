# Projet TrueNAS Scale

## Description
Ce projet consiste à installer et configurer TrueNAS Scale sur une machine virtuelle (VM) ainsi qu'une deuxième VM Debian avec interface graphique. Nous avons également mis en place un système de stockage RAID 6 et installé l'application Vaultwarden pour la gestion des mots de passe.

---

## Prérequis

### Configuration de la VM TrueNAS Scale
- **Processeur** : 2 cœurs
- **Mémoire vive (RAM)** : 4 Go
- **Disques durs (DD)** : 2 de 16 Go
- **Disques durs supplémentaires** : 5 de 2 Go, combinés en un espace de stockage de 2 Go via un RAID 6 logiciel.

### Configuration de la deuxième VM (Debian)
- **Processeur** : 2 cœurs
- **Mémoire vive (RAM)** : 2 Go
- **Disques durs (DD)** : 1 de 8 Go

---

## Installation et Configuration

### Mise en place du RAID 6
Nous avons créé un RAID 6 avec les 5 disques de 2 Go et l'avons nommé **"stockage"**.

<img src="/screen/1.png" alt="Capture d'écran"/>

### Création et gestion des utilisateurs
- Ajout d'un stockage.
- Création d'un dataset pour chaque utilisateur.
- Création d'un groupe d'utilisateurs pour la gestion des droits.

### Sécurisation et Accès à TrueNAS
- Connexion sécurisée en **HTTPS**.
- Activation des services **SSH** et **FTP** via **Système > Services**.

<img src="/screen/2.png" alt="Capture d'écran"/>

- Configuration du SSH :
  - Modification du port.
  - Ajout du SSH à un groupe dédié.
- Vérification du bon fonctionnement avec la deuxième machine virtuelle Debian.

<img src="/screen/3.png" alt="Capture d'écran"/>

### Installation de Vaultwarden

<img src="/screen/4.png" alt="Capture d'écran"/>

1. Création d'un stockage sur un disque de 16 Go.
2. Création d'un dataset "Application".
3. Téléchargement et installation de **Vaultwarden**.
4. Configuration avec deux mots de passe.
5. Vérification de l'installation :
   - Accès à la partie **Admin**.
   - Création d'un compte principal via le **Web UI**.

<img src="/screen/5.png" alt="Capture d'écran"/>
  
6. Installation de l'extension **Bitwarden** sur Chrome pour la gestion des mots de passe.

<img src="/screen/7.png" alt="Capture d'écran"/>

### Création d'une VM Debian sur TrueNAS Scale
1. Désactiver **Hyper-V** sur Windows avec la commande :
   ```powershell
   bcdedit /set hypervisorlaunchtype off
   ```
2. Désactiver l'intégrité de la mémoire :
   - Rechercher **"Isolation du noyau"** dans la barre de recherche Windows.
   - Désactiver **l'intégrité de la mémoire**.
3. Dans les paramètres de la VM, activer :
   - **Virtualize Intel VT-x/EPT or AMD-V/RVI**.
4. Redémarrer l'ordinateur.
5. Création de la VM Debian sur TrueNAS Scale :
   - Ajouter l'ISO dans un dataset partagé en **SMB**.

<img src="/screen/8.png" alt="Capture d'écran"/>

   - Définir le **chargeur d'amorçage** sur **UEFI_CSM**.
   - Régler le **délai d'arrêt** à 300 sec pour permettre l'installation de l'ISO (modifiable ultérieurement).

<img src="/screen/9.png" alt="Capture d'écran"/>

<img src="/screen/10.png" alt="Capture d'écran"/>
