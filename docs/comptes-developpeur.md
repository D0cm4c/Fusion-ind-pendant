# Comptes développeur des API tierces — procédure

Ces comptes appartiennent au propriétaire du projet (créés dans ses propres consoles Google / Microsoft / Dropbox…). **Aucun secret ne doit jamais entrer dans le code ni dans git** : tout passe par un fichier `.env` à la racine, listé dans `.gitignore`, chargé uniquement dans le process main d'Electron.

## Google (Gmail API + Drive API)

1. [Google Cloud Console](https://console.cloud.google.com) → nouveau projet
2. Activer **Gmail API** et **Drive API**
3. Écran de consentement OAuth : mode « Test » au début (testeurs = ton adresse) ; pour une diffusion publique, soumettre la vérification Google (scopes Gmail = restricted, revue CASA possible)
4. Identifiants → créer « ID client OAuth » de type **Application de bureau** → redirect `http://127.0.0.1`
5. Copier `client_id` / `client_secret` → `.env` : `GOOGLE_CLIENT_ID`, `GOOGLE_CLIENT_SECRET`
6. Scopes demandés : `gmail.modify`, `gmail.send`, `drive.file`, `userinfo.email`

## Microsoft (Outlook / Graph)

1. [Azure Portal](https://portal.azure.com) → Inscriptions d'applications → Nouvelle inscription (comptes perso + pro : endpoint `/common`)
2. Redirect URI : `http://localhost` (PKCE, **pas de secret client** pour une app desktop publique)
3. API autorisées (déléguées) : `User.Read`, `Mail.ReadWrite`, `Mail.Send`, `offline_access`
4. Copier l'ID d'application → `.env` : `MS_CLIENT_ID`

## Dropbox

1. [Dropbox App Console](https://www.dropbox.com/developers/apps) → Create app → « Scoped access » / Full Dropbox
2. Permissions : `files.content.read`, `files.content.write`
3. Redirect : `http://127.0.0.1:<port fixe>` (PKCE)
4. `.env` : `DROPBOX_CLIENT_ID`

## Fournisseurs « vie privée » (M2+)

- **pCloud** : console développeur pCloud → app → OAuth2, redirect 127.0.0.1
- **MEGA** : SDK officiel (compte MEGA, app enregistrée)
- **kDrive** : API ownCloud-like d'Infomaniak + mot de passe d'application
- **Nextcloud / Icedrive / Koofr…** : WebDAV + mot de passe d'application (pas d'OAuth centralisé)
- **Proton Drive** : API encore jeune — à réévaluer au moment du dev

## Fichier `.env` (exemple de forme, valeurs à remplir)

```
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
MS_CLIENT_ID=
DROPBOX_CLIENT_ID=
```

`.gitignore` doit contenir `.env`, `*.db`, `*.db.bak`, `dist/`, `node_modules/`.

## Stockage des tokens dans l'app

Jamais en clair : `safeStorage.encryptString()` (Keychain / Credential Manager / libsecret), stockés dans la table `compte_connexion.tokens_chiffres`. Le mot de passe maître (SQLCipher) ne passe jamais par le réseau.
