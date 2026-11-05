# Onboarding — le premier lancement

Objectif : qu'un débutant soit opérationnel en quelques minutes, sans jamais être bloqué. Chaque étape peut être sautée (« Plus tard ») et reprise ensuite depuis la checklist d'accueil.

## Parcours étape par étape (une seule question par écran)

1. **Bienvenue** — en trois phrases, ce que fait l'application (le flux recevoir → classer → suivre le temps → facturer → être payé) et la promesse « rien ne bouge sans votre validation »
2. **Où stocker vos fichiers ?** (aucun enregistrement développeur requis en MVP)
   - [Nextcloud / Koofr / Icedrive / ownCloud — WebDAV] — adresse + mot de passe d'application, zéro configuration côté fournisseur
   - [Un dossier de mon ordinateur] — mode **100 % local** : aucun compte cloud requis, les fichiers restent sur la machine (dossier au choix, emplacement proposé par défaut)
   - [Google Drive / Dropbox / kDrive / pCloud / MEGA / Proton Drive] — via API officielle : nécessite un enregistrement développeur (option avancée, voir [comptes-developpeur.md](comptes-developpeur.md))
   - [Plus tard]

2b. **Créez votre mot de passe maître** — obligatoire dans tous les cas, même en mode 100 % local : il chiffre la base de données **et le cache des pièces jointes** (et permet la synchro chiffrée si cloud). Il ne quitte jamais l'ordinateur — une **phrase de récupération imprimable** est proposée. Voir [synchro-chiffree.md](synchro-chiffree.md)
3. **Quelle boîte mail connecter ?** (IMAP/SMTP, aucun enregistrement requis)
   - saisir l'adresse mail → **détection automatique des serveurs** (Gmail avec mot de passe d'application, Orange, Free, SFR, Bouygues, La Poste, OVH, Infomaniak, Yahoo, iCloud, Zoho…) ou saisie guidée ; le **mot de passe d'application** est expliqué pas à pas quand le fournisseur l'exige
   - [Outlook / Microsoft 365] — via Microsoft Graph (OAuth) : option avancée nécessitant un enregistrement Azure, voir [comptes-developpeur.md](comptes-developpeur.md)
   - [Plus tard]
4. **Un chat à connecter ?** (optionnel) — [Telegram] [Discord] [Plus tard]
5. **Votre premier projet** — nom du projet, nom du client, taux horaire par défaut
6. **C'est prêt** — récapitulatif en checklist (Stockage ✓ / Mot de passe maître ✓ / Mail ✓ / …) avec le bouton « Ouvrir mon espace »

## Règles UX

- Une seule question par écran, gros boutons explicites, langage clair
- « Plus tard » toujours proposé : l'application fonctionne entièrement en local sans aucun compte externe
- La checklist d'accueil reste visible jusqu'à ce que chaque élément soit fait
- En cas d'échec de connexion : cause probable expliquée + nouvelle tentative guidée, jamais un code d'erreur brut
- Les identifiants saisis (IMAP) sont chiffrés via `safeStorage` comme les tokens OAuth
