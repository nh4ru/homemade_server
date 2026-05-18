# 🖥️ Homemade NAS Server

> Mise en place d'un serveur NAS homemade sous Ubuntu Desktop 24.04 LTS avec partage réseau Samba, interface de gestion Cockpit et Wake-on-LAN.

---

## 📋 Table des matières

- [Matériel](#matériel)
- [Logiciels](#logiciels)
- [Étape 1 — Création de la clé USB bootable](#étape-1--création-de-la-clé-usb-bootable)

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
