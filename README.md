# Fusion Indépendant

Application **desktop installable** qui aide un indépendant — y compris quelqu'un qui n'est pas à l'aise avec l'informatique — à administrer ses projets en un seul endroit.

## Les quatre piliers

1. **Fichiers & images** — classement et tri intelligents des fichiers reçus (mail, chat, dépôt manuel), stockés sur votre propre cloud (Google Drive, Dropbox, ou un fournisseur plus confidentiel : kDrive, pCloud, MEGA, Proton Drive, Nextcloud…). Voir [docs/classement-intelligent.md](docs/classement-intelligent.md)
2. **Messages** — boîte mail unifiée (Gmail, Outlook, ou toute autre boîte mail via IMAP) et chat (Telegram, Discord), reliée à chaque projet et chaque client
3. **Temps** — suivi du temps passé par projet et par tâche (minuteur, timesheet)
4. **Facturation** — devis et factures générés depuis le temps passé, envoyés par mail, suivi des paiements
5. **Notes & base de connaissances** — notes de réunion rattachées à chaque projet (minuteur intégré, actions à faire), notes reliées entre elles façon base de connaissances (liens proposés automatiquement, comme Obsidian mais sans syntaxe à apprendre), et fil de commentaires sur chaque fichier. Voir [docs/notes-reunions.md](docs/notes-reunions.md)

## Le problème que l'on résout

Pour un indépendant, le stress vient de la dispersion : fichiers et échanges éparpillés entre la boîte mail, les téléchargements, Drive et Dropbox — et heures ou factures oubliées. L'application y répond par un **seul flux continu** :

**recevoir → classer → suivre le temps → facturer → être payé**

Le classement intelligent des fichiers (pilier 1) est la porte d'entrée de ce flux : c'est souvent un fichier reçu par mail qui crée le lien client → projet, et tout le reste en découle.

**Fiche client** : chaque client a sa fiche récapitulative avec un tableau de bord — travail fait, reste à faire, fichiers arrivés, fichiers à envoyer — généré à partir des notes, fichiers, tâches, temps et factures (pas d'agent IA : l'app agrège les données existantes et encourage à compléter ce qui manque via une jauge de complétude et des rappels doux). Voir [docs/fiche-client.md](docs/fiche-client.md)

**To-do list centrale** : les tâches du jour vivent au cœur de l'écran d'accueil « Aujourd'hui », reliées aux fichiers, mails, notes de réunion et fiches clients (liens bidirectionnels). Voir [docs/taches.md](docs/taches.md)

## Principes directeurs

- **Desktop installable** : installateurs natifs Windows / macOS / Linux, données en local (SQLite), fonctionnement possible hors ligne
- **Pensé pour les débutants** : assistant de connexion pas à pas, une seule action par écran, langage clair, explications à chaque étape
- **Rien ne bouge sans vous** : l'application *propose* de ranger et d'étiqueter chaque fichier reçu, mais n'applique jamais une suggestion sans votre clic de validation (mode prudent par défaut)
- **Stockage au choix dès l'installation** : Google Drive, Dropbox, un fournisseur respectueux de la vie privée (kDrive, pCloud, MEGA, Proton Drive, Nextcloud…), ou un simple dossier de votre ordinateur (mode 100 % local, aucun compte cloud requis)
- **Un écran d'accueil utile** : « Aujourd'hui », centré sur **se mettre au travail** — tâches du jour, intervention/RDV du jour, messages à traiter, en attente d'argent — avec la boîte à classer en compteur secondaire — voir [docs/ecran-accueil.md](docs/ecran-accueil.md) et [docs/personas.md](docs/personas.md)
- **Synchro multi-postes chiffrée** : le cloud sert aussi à synchroniser l'app entre plusieurs ordinateurs, via un fichier chiffré (mot de passe maître, jamais transmis) — voir [docs/synchro-chiffree.md](docs/synchro-chiffree.md)
- **Vos comptes, vos données** : connexion OAuth à vos propres comptes Google Drive / Dropbox / Gmail / Outlook ; les identifiants sont chiffrés dans le trousseau de votre système, jamais stockés en clair

## Stack

Electron + Vite + React + TypeScript, SQLite (`better-sqlite3`), empaquetage `electron-builder`, OAuth2 + PKCE avec retour sur `127.0.0.1`.

## Documentation

- [Benchmark des applications existantes](docs/concurrents.md)
- [Écran d'accueil — point pivot](docs/ecran-accueil.md)
- [Personas : croisement plombier / architecte / webdesigner](docs/personas.md)
- [Synchro multi-postes chiffrée](docs/synchro-chiffree.md)
- [Fiche client et tableau de bord](docs/fiche-client.md)
- [To-do list centrale et reliée](docs/taches.md)
- [Onboarding (premier lancement)](docs/onboarding.md)
- [Architecture et connecteurs](docs/architecture.md)
- [Classement intelligent des fichiers](docs/classement-intelligent.md)
- [Notes de réunion et commentaires](docs/notes-reunions.md)
- [Phasage](docs/phasage.md)
