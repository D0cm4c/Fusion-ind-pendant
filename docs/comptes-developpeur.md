# Connexion aux services tiers : faut-il des « comptes développeur » ?

## GitHub ne suffit pas — pourquoi ?

GitHub héberge **le code** de l'application (dépôt, PR, issues — c'est là qu'est notre PR #1). Mais quand l'app veut lire **vos** mails ou **vos** fichiers, ce sont Google / Microsoft / Dropbox qui les gardent, et ils ne laissent aucune application y accéder sans identification. Il faudrait alors enregistrer l'app une fois dans leur console (Google Cloud Console, Azure Portal, Dropbox App Console) pour recevoir une clé OAuth (`client_id`) — gratuit et rapide (~10 min), mais **obligatoire** pour utiliser leurs API officielles.

## Mode retenu pour le MVP : zéro compte développeur

Les **protocoles ouverts** ne demandent aucun enregistrement :

- **Mail : IMAP (lecture) + SMTP (envoi)** avec adresse + mot de passe, ou **mot de passe d'application** quand le fournisseur l'exige — Gmail fonctionne en IMAP avec un mot de passe d'application, idem Orange, Free, SFR, OVH, Infomaniak, Yahoo, iCloud. Détection automatique des serveurs à partir de l'adresse, comme Thunderbird.
  - Limite connue : **Outlook.com / Microsoft 365 moderne a retiré l'authentification basique** → nécessite OAuth, donc un enregistrement Azure. Proposé en option avancée.
- **Stockage fichiers : WebDAV** (Nextcloud, Koofr, Icedrive, ownCloud, kDrive payant…) avec mot de passe d'application, ou **dossier local**. Google Drive / Dropbox sans API officielle sont impossibles en mode zéro-enregistrement.
- Avantage : l'utilisateur n'a **rien à créer**, l'app fonctionne immédiatement.

## Mode optionnel (M2+) : API officielles via comptes développeur

Utile pour : Gmail API (labels, recherche plein texte, pièces jointes natives, notifications push), Microsoft Graph (Outlook moderne), Drive / Dropbox API (métadonnées riches, partage, corbeille distante).

Procédure quand on voudra l'activer :

1. **Google** — [Cloud Console](https://console.cloud.google.com) → projet → activer Gmail API + Drive API → identifiants OAuth « Application de bureau », redirect `http://127.0.0.1` → `GOOGLE_CLIENT_ID` / `GOOGLE_CLIENT_SECRET` dans `.env`. Mode « Test » suffisant en perso ; vérification Google (CASA) nécessaire uniquement en diffusion publique (scopes Gmail restricted).
2. **Microsoft** — [Azure Portal](https://portal.azure.com) → inscription d'app, endpoint `/common`, redirect `http://localhost`, permissions déléguées `User.Read Mail.ReadWrite Mail.Send offline_access`, PKCE sans secret → `MS_CLIENT_ID` dans `.env`.
3. **Dropbox** — [App Console](https://www.dropbox.com/developers/apps) → app « Scoped access », permissions `files.content.read/write`, redirect `http://127.0.0.1:<port>` → `DROPBOX_CLIENT_ID` dans `.env`.

## Règle absolue sur les secrets

Aucun secret dans le code ni dans git : uniquement un fichier `.env` à la racine (dans `.gitignore`), chargé dans le process main d'Electron. Les tokens OAuth sont chiffrés via `safeStorage` (table `compte_connexion.tokens_chiffres`). Le mot de passe maître (SQLCipher) ne transite jamais par le réseau.
