# Fusion Indépendant

Application **desktop installable** qui aide un indépendant — y compris quelqu'un qui n'est pas à l'aise avec l'informatique — à administrer ses projets en un seul endroit.

## Les quatre piliers

1. **Fichiers & images** — classement et tri intelligents des fichiers reçus (mail, chat, dépôt manuel), stockés sur votre propre Google Drive ou Dropbox. Voir [docs/classement-intelligent.md](docs/classement-intelligent.md)
2. **Messages** — boîte mail unifiée (Gmail, Outlook) et chat (Telegram, Discord), reliée à chaque projet et chaque client
3. **Temps** — suivi du temps passé par projet et par tâche (minuteur, timesheet)
4. **Facturation** — devis et factures générés depuis le temps passé, envoyés par mail, suivi des paiements

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
- [Phasage](docs/phasage.md)
