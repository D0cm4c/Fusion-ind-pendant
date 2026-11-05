# Synchronisation multi-postes via un fichier chiffré

Objectif : utiliser le Drive / Dropbox non seulement comme stockage de fichiers, mais comme **outil de synchronisation entre plusieurs ordinateurs** — via un **fichier chiffré**, pour que le fournisseur (Google, Dropbox) ne voie jamais les données en clair. On peut ainsi utiliser un Google Drive sans crainte que ces données soient lisibles par Google.

## Principe

- La base SQLite est chiffrée au repos avec **SQLCipher** (AES-256). La clé est dérivée d'un **mot de passe maître** saisi sur chaque poste (Argon2id/PBKDF2, sel aléatoire dans l'en-tête du fichier)
- Le mot de passe maître **ne quitte jamais l'ordinateur** : jamais transmis, jamais stocké en clair. La synchro sur un nouveau poste demandera de le ressaisir
- Le fichier chiffré `fusion.db` est déposé dans `Fusion/_sync/` sur le stockage cloud connecté ; l'autre poste le télécharge, le déchiffre localement et travaille dessus

## Règles de synchro (MVP, usage solo)

- Synchronisation au lancement de l'app, à sa fermeture, et via un bouton « Synchroniser maintenant »
- **Last-write-wins** sur le fichier entier : comparaison du hash + horodatage, le plus récent gagne
- **Conflit** (les deux postes ont modifié depuis la dernière synchro) : on conserve les deux versions sur le cloud (`fusion.db` + `fusion-conflit-<date>.db`) et on notifie l'utilisateur, qui choisit laquelle garder — jamais de fusion automatique silencieuse
- Copie de sécurité locale `.bak` avant chaque remplacement

## Mot de passe maître

- Créé à l'onboarding **dans tous les cas** (même en mode 100 % local) : la base est toujours chiffrée, avec saisie double de confirmation
- Explication en clair à l'utilisateur : « ce mot de passe ne quitte jamais votre ordinateur ; il sert à chiffrer vos données avant qu'elles ne partent sur le cloud »
- Mot de passe oublié = données irrécupérables (c'est le prix de l'anonymat) → une **phrase de récupération** est générée localement à la création, à imprimer et conserver hors ligne
- Option « se souvenir sur ce poste » via `safeStorage` (confort local uniquement)

## Limites honnêtes

- La **base de données** (métadonnées des fichiers, index des mails, projets, clients, temps, factures, notes) **et le cache des pièces jointes** sont chiffrés — rien n'est jamais écrit en clair sur le disque. Les fichiers eux-mêmes restent sur le cloud, noms visibles par le fournisseur — sauf option avancée « coffre-fort » (chiffrement individuel des fichiers sensibles, envisagée post-M4)
- La synchro n'est pas en temps réel : deux postes ouverts simultanément peuvent entrer en conflit (géré ci-dessus)

## Fichiers concernés

- Distant : `Fusion/_sync/fusion.db` (chiffré SQLCipher) + horodatage/hash
- Local : base de l'app + `fusion.db.bak` (sécurité avant remplacement)
