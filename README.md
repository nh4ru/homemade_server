# 🖥️ Homemade NAS Server

> Mise en place d'un serveur NAS homemade sous Ubuntu Desktop 24.04 LTS avec partage réseau Samba, interface de gestion Cockpit et Wake-on-LAN.

---

## 📋 Table des matières

- [Matériel](#matériel)
- [Logiciels](#logiciels)
- [Étape 1 — Création de la clé USB bootable](#étape-1--création-de-la-clé-usb-bootable)
- [Étape 2 — Installation d'Ubuntu Desktop 24.04 LTS]
- [Étape 3 — Mise à jour du système]
- [Étape 4 — Installation et configuration de Cockpit]
- [Étape 5 — Installation du driver NVIDIA]
- [Étape 6 — Installation et configuration de Samba]
- [Étape 7 — Montage automatique des disques]  

---

## 🔧 Matériel

| Composant | Détail |
|---|---|
| CPU | Intel i5 6600K |
| RAM | 16GB DDR4 |
| Carte mère | ASUS Maximus Hero VIII |
| SSD (système) | Samsung 980 1TB |
| HDD stockage principal | HGST 3TB 7200RPM (HDN724030ALE640) |
| HDD stockage secondaire | Seagate Barracuda 250GB (ST3250318AS) |

---

## 💿 Logiciels

| Logiciel | Rôle |
|---|---|
| Ubuntu Desktop 24.04 LTS | Système d'exploitation |
| Cockpit | Interface de gestion web |
| Samba | Partage réseau |
| SSH | Accès distant |

---

## Étape 1 — Création de la clé USB bootable

**Objectif :** Préparer le support d'installation d'Ubuntu Desktop 24.04 LTS.

**Outils utilisés :**
- [Ubuntu Desktop 24.04 LTS](https://ubuntu.com/download/desktop)
- [Rufus](https://rufus.ie)

**Paramètres Rufus :**

| Paramètre | Valeur |
|---|---|
| Schéma de partition | GPT |
| Système cible | UEFI (non CSM) |
| Système de fichiers | FAT32 |
| Mode d'écriture | Mode ISO |

**Matériel :** Clé USB 8GB minimum

**Résultat :** Clé USB bootable UEFI prête pour l'installation.

## Étape 2 — Installation d'Ubuntu Desktop 24.04 LTS

**Objectif :** Installer le système d'exploitation.

**Paramètres d'installation :**

| Paramètre | Valeur |
|---|---|
| Type d'installation | Interactive |
| Version | Complète |
| Logiciels propriétaires | Activés (drivers NVIDIA + codecs multimédia) |

**Résultat :** Ubuntu Desktop 24.04.4 LTS installé sur Samsung 980 1TB.

---

## Étape 3 — Mise à jour du système

```bash
sudo apt update && sudo apt upgrade -y
```

**Résultat :** Système à jour.

---

## Étape 4 — Installation et configuration de Cockpit

**Objectif :** Mettre en place une interface web de gestion du serveur.

```bash
sudo apt install cockpit
sudo systemctl enable --now cockpit.socket
```

**Accès :** `http://localhost:9090` ou `http://192.168.1.17:9090`

**Résultat :** Interface Cockpit accessible et opérationnelle.

---

## Étape 5 — Installation du driver NVIDIA

```bash
ubuntu-drivers devices  # identifier le driver recommandé
sudo apt install nvidia-driver-535 -y
```

**Driver installé :** 535.309.01 — GTX 1050 Ti détectée et opérationnelle.

---

## Étape 6 — Installation et configuration de Samba

**Objectif :** Partager les disques de stockage sur le réseau local.

```bash
sudo apt install samba
sudo systemctl enable --now smbd
```

**Configuration des partages** (`/etc/samba/smb.conf`) :

```ini
[Films]
path = /mnt/stockage_250gb
browseable = yes
writable = yes
guest ok = yes

[Données]
path = /mnt/stockage_3tb
browseable = yes
writable = yes
guest ok = yes
```

**Création utilisateur Samba :**
```bash
sudo smbpasswd -a nharu
```

**Résultat :** Partages accessibles depuis Windows via `\\192.168.1.17`.

---

## Étape 7 — Montage automatique des disques

**Objectif :** Monter les disques de stockage automatiquement au démarrage.

```bash
sudo mkdir -p /mnt/stockage_3tb
sudo mkdir -p /mnt/stockage_250gb
```

**Configuration** (`/etc/fstab`) :
