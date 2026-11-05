# Fusion Indépendant

Application **desktop installable** qui aide un indépendant — y compris quelqu'un qui n'est pas à l'aise avec l'informatique — à administrer ses projets en un seul endroit.

## Les quatre piliers

1. **Fichiers & images** — classement et tri intelligents des fichiers reçus (mail, chat, dépôt manuel), stockés sur votre propre Google Drive ou Dropbox. Voir [docs/classement-intelligent.md](docs/classement-intelligent.md)
2. **Messages** — boîte mail unifiée (Gmail, Outlook) et chat (Telegram, Discord), reliée à chaque projet et chaque client
3. **Temps** — suivi du temps passé par projet et par tâche (minuteur, timesheet)
4. **Facturation** — devis et factures générés depuis le temps passé, envoyés par mail, suivi des paiements
5. **Notes de réunion & commentaires** — prise de notes pendant les réunions, rattachée à chaque projet (avec minuteur intégré et actions à faire), et fil de commentaires sur chaque fichier. Voir [docs/notes-reunions.md](docs/notes-reunions.md)

## Le problème que l'on résout

Pour un indépendant, le stress vient de la dispersion : fichiers et échanges éparpillés entre la boîte mail, les téléchargements, Drive et Dropbox — et heures ou factures oubliées. L'application y répond par un **seul flux continu** :

**recevoir → classer → suivre le temps → facturer → être payé**

Le classement intelligent des fichiers (pilier 1) est la porte d'entrée de ce flux : c'est souvent un fichier reçu par mail qui crée le lien client → projet, et tout le reste en découle.

## Principes directeurs

- **Desktop installable** : installateurs natifs Windows / macOS / Linux, données en local (SQLite), fonctionnement possible hors ligne
- **Pensé pour les débutants** : assistant de connexion pas à pas, une seule action par écran, langage clair, explications à chaque étape
- **Rien ne bouge sans vous** : l'application *propose* de ranger et d'étiqueter chaque fichier reçu, mais n'applique jamais une suggestion sans votre clic de validation (mode prudent par défaut)
- **Vos comptes, vos données** : connexion OAuth à vos propres comptes Google Drive / Dropbox / Gmail / Outlook ; les identifiants sont chiffrés dans le trousseau de votre système, jamais stockés en clair

## Stack

Electron + Vite + React + TypeScript, SQLite (`better-sqlite3`), empaquetage `electron-builder`, OAuth2 + PKCE avec retour sur `127.0.0.1`.

## Documentation

- [Architecture et connecteurs](docs/architecture.md)
- [Classement intelligent des fichiers](docs/classement-intelligent.md)
- [Notes de réunion et commentaires](docs/notes-reunions.md)
- [Phasage](docs/phasage.md)
