# Architecture

## Stack

- **Electron** (process main + renderer), **Vite**, **React**, **TypeScript**
- **SQLite** via `better-sqlite3` : toutes les données métier en local, l'app fonctionne hors ligne
- **electron-builder** : installateurs natifs (`.exe`/`.msi` Windows, `.dmg` macOS, `.AppImage`/`.deb` Linux) + auto-update optionnel
- **OAuth2 + PKCE** pour toutes les connexions, avec redirect sur un serveur local `127.0.0.1` : l'utilisateur se connecte dans son navigateur habituel, l'app récupère le retour toute seule
- **safeStorage** : tokens et secrets chiffrés via le trousseau du système (Keychain macOS, Credential Manager Windows, libsecret Linux), jamais écrits en clair sur le disque

## Connecteurs (vos comptes, vos données)

**Voie principale du MVP (zéro enregistrement développeur) : IMAP/SMTP pour le mail, WebDAV ou dossier local pour les fichiers.** Les API officielles Google / Microsoft / Dropbox (Drive, Gmail API, Graph) sont des options M2+ nécessitant un compte développeur — voir [comptes-developpeur.md](comptes-developpeur.md).

| Service | API | Scopes / permissions | Notes |
|---|---|---|---|
| Google Drive | Drive API v3 | `drive.file` ou `drive` | **option M2+** (compte développeur) ; dossier racine dédié `Fusion/` |
| Dropbox | Content API | OAuth2 + PKCE | **option M2+** (compte développeur) ; dossier racine `Fusion/` |
| kDrive (Infomaniak) | API kDrive (compatible ownCloud) | Suisse, 15 Go gratuits | hébergement souverain, option « vie privée » |
| pCloud | pCloud API | Suisse, 10 Go gratuits | chiffrement côté client en option (Crypto) |
| MEGA | MEGA SDK / API | 20 Go gratuits, chiffrement de bout en bout natif | API officielle, E2EE par défaut |
| Proton Drive | API Proton (encore jeune — à confirmer au moment du dev) | Suisse, 5 Go gratuits, zero-knowledge | chiffrement de bout en bout natif |
| Nextcloud / ownCloud / Icedrive / Koofr / autres | **WebDAV** (un seul connecteur couvre ces fournisseurs) | mot de passe d'application, auto-hébergé possible | open source, hébergement au choix |
| Gmail | **IMAP/SMTP en MVP** (mot de passe d'application) ; Gmail API en option M2+ | `gmail.modify`, `gmail.send` pour l'API | API = scopes « restricted », vérification Google (CASA) si diffusion publique |
| Outlook / Microsoft 365 | **Microsoft Graph en option M2+** (compte développeur Azure ; IMAP impossible, Basic Auth retiré) | `Mail.ReadWrite Mail.Send offline_access`, endpoint `/common` | consentement de l'utilisateur seul |
| Toute autre boîte mail (Orange, Free, SFR, Bouygues, La Poste, OVH, Infomaniak, Yahoo, iCloud, Zoho…) | **IMAP** (lecture) + **SMTP** (envoi), OAuth2 quand le fournisseur le propose, sinon mot de passe / mot de passe d'application | détection automatique des serveurs, ou saisie guidée ; identifiants chiffrés via safeStorage |
| Telegram | Bot API (bot, gratuit) ou MTProto compte utilisateur (GramJS) | api_id/api_hash pour le compte | gratuit ; les clients non officiels sont surveillés (risque flood/ban en cas d'abus) |
| Discord | API officielle (bot) | bot + scopes messages | gratuit, stable |
| WhatsApp | **pas d'API pour les comptes personnels** | — | option 1 : lien `wa.me` « ouvrir dans WhatsApp » (légal, gratuit) ; option 2 : WhatsApp Business Cloud API (numéro dédié + Meta Business vérifié, facturation au message livré depuis juillet 2025, templates approuvés pour démarrer une conversation) — module avancé, payant |

## Données

- **Base SQLite locale** : projets, clients, fichiers (métadonnées), index des messages, temps, devis/factures, règles de classement apprises
- **Fichiers binaires** : au choix — sur le Google Drive / Dropbox de l'utilisateur, **ou dans un dossier local de l'ordinateur** (mode 100 % local, choisi à l'onboarding) ; sauvegarde chiffrée optionnelle de la base sur le stockage cloud connecté
- **Sécurité** : scopes minimaux demandés, aucune suppression automatique, corbeille avant toute destruction, journal d'activité de chaque action
- **Synchro multi-postes** : base chiffrée (SQLCipher + mot de passe maître) déposée dans `Fusion/_sync/` sur le cloud, last-write-wins avec détection de conflit — voir [synchro-chiffree.md](synchro-chiffree.md)

## Messageries : le bilan honnête

- Mail Gmail + Outlook : intégration officielle, gratuite, fiable → cœur du module Messages
- Telegram, Discord : API officielles gratuites → chat intégré
- WhatsApp compte perso : **aucune API officielle** ; les solutions non officielles (QR multi-device) violent les CGU et risquent le bannissement du numéro → on ne le promet pas dans l'app
- Signal : pas d'API officielle (`signal-cli` non officiel) ; iMessage : impossible proprement

## UX « débutant d'abord »

- Assistant de première configuration avec checklist visible en permanence — parcours détaillé dans [onboarding.md](onboarding.md) : choix du stockage (Drive / Dropbox / **local** / plus tard), choix de la messagerie (Gmail / Outlook / **autre adresse IMAP** / plus tard), chat optionnel, premier projet
- Une seule action par écran, boutons explicites (« Connecter mon compte Gmail »), jamais de jargon technique
- Chaque connexion explique en clair à quoi elle donne accès, avec bouton « Révoquer »
- En cas d'erreur : cause probable + étape suivante proposées, jamais un code d'erreur brut
- Mode simplifié (par défaut) / mode avancé (réglages puissants, classement automatique) derrière un toggle
