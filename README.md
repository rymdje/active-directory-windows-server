# Contrôleur de domaine Active Directory - Windows Server 2022

Projet personnel que j'ai réalisé pour m'entraîner sur les systèmes et réseaux, dans le cadre de ma préparation au Titre Pro TSSR.

L'idée était de monter un petit environnement d'entreprise de zéro : un serveur Windows Server, un domaine Active Directory, des utilisateurs, des groupes et quelques règles de sécurité. Le tout dans des machines virtuelles sur mon PC.

## Le contexte

J'ai imaginé une petite entreprise fictive de 16 personnes réparties en 4 services (direction, comptabilité, informatique, commercial). L'objectif : mettre en place l'infrastructure qui permet de gérer tous ces comptes de façon centralisée, comme dans une vraie boîte.

Domaine : `rym.local`

## Ce que j'ai utilisé

- VirtualBox pour la virtualisation
- Windows Server 2022 (version d'évaluation)
- 1 serveur : SRV-AD01, en IP fixe (192.168.10.10)

## Comment c'est organisé
rym.local
└── Datalex

├── Direction (2 utilisateurs)

├── Comptabilité (4 utilisateurs)

├── Informatique (3 utilisateurs)

├── Commercial (7 utilisateurs)

└── Groupes

├── GS_Direction

├── GS_Comptabilité

├── GS_Informatique

└── GS_Commercial
Les groupes servent à gérer les droits par service plutôt que personne par personne.

## Les étapes

1. **Installation du serveur** : install de Windows Server 2022, renommage en SRV-AD01, configuration d'une adresse IP fixe et du DNS.

2. **Active Directory** : installation du rôle AD DS puis promotion du serveur en contrôleur de domaine, ce qui crée le domaine rym.local.

3. **Les comptes** : création des unités d'organisation (une par service), des 16 utilisateurs rangés dans le bon service, et des 4 groupes de sécurité.

4. **Sécurité (GPO)** : j'ai mis en place trois stratégies de groupe.
   - une politique de mot de passe (10 caractères minimum, complexité obligatoire, renouvellement tous les 90 jours)
   - le verrouillage automatique des sessions après 10 min d'inactivité
   - un message d'avertissement à la connexion

## Captures

Les captures des différentes étapes sont dans le dossier `captures`.

## Ce que ça m'a appris

- installer et prendre en main Windows Server
- configurer un réseau simple (IP statique, DNS)
- installer et gérer Active Directory
- créer et organiser des comptes et des groupes
- mettre en place des GPO
- documenter un projet correctement

J'ai fait la création des comptes à la main ici pour bien comprendre le fonctionnement. Je compte refaire la même chose en PowerShell dans un prochain projet pour montrer la partie automatisation.
