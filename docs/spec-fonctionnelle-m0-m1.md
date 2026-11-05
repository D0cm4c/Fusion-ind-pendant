# Spécification fonctionnelle — M0 & M1

Document de référence avant le premier code : on ne code que ce qui est écrit ici. Wireframes textuels (pas besoin de maquettes graphiques à ce stade).

## User stories prioritaires

**M0**
- US1 — En tant qu'indépendant débutant, je veux installer l'app et terminer l'onboarding en moins de 10 minutes, sans aide extérieure
- US2 — Je veux choisir mon stockage (Drive / Dropbox / cloud privé / dossier local) et ma messagerie (Gmail / Outlook / autre IMAP), étape par étape, avec « Plus tard » proposé à chaque étape
- US3 — Je veux créer mon premier projet (nom, client, taux horaire)

**M1**
- US4 — Je veux voir tous mes mails dans une liste unifiée, lire un mail, répondre / envoyer depuis l'app
- US5 — Je veux que chaque pièce jointe reçue apparaisse dans « À classer » avec une proposition de dossier + étiquettes, applicable en un clic
- US6 — Je veux un écran d'accueil « Aujourd'hui » (tâches du jour, messages à traiter, à classer, en attente d'argent)

## Écrans M0 (onboarding)

- **E0 — Bienvenue** : 3 phrases du flux (recevoir → classer → temps → facturer → être payé) + promesse « rien ne bouge sans votre validation » + [Commencer]
- **E1 — « Où stocker vos fichiers ? »** : boutons en liste — Google Drive / Dropbox / kDrive / pCloud / MEGA / Proton Drive / Nextcloud-WebDAV / 📁 Dossier de mon ordinateur / Plus tard
  - si cloud → **E1b Mot de passe maître** : champ + confirmation + explication « ne quitte jamais cet ordinateur » + [Imprimer ma phrase de récupération]
  - puis **E1c Connexion OAuth** : « Ouvrir dans mon navigateur… » → retour automatique (127.0.0.1) → « ✅ C'est connecté » ou erreur expliquée + [Réessayer]
  - si local → **E1d** choix du dossier (emplacement proposé par défaut)
- **E2 — « Quelle boîte mail connecter ? »** (IMAP/SMTP, zéro enregistrement) : champ adresse mail + [Connecter] → **détection automatique des serveurs** (Gmail avec mot de passe d'application, Orange, Free, SFR, OVH, Infomaniak, Yahoo, iCloud…) ou saisie guidée (serveurs, ports, sécurité) → mot de passe / mot de passe d'application expliqué pas à pas → [Tester la connexion] → ✅ ou erreur en langage clair
  - [Outlook / Microsoft 365] proposé en option avancée (OAuth Microsoft — voir [comptes-developpeur.md](comptes-developpeur.md)) ; [Plus tard]
- **E3 — « Un chat à connecter ? »** (optionnel) : [Telegram] [Discord] [Plus tard]
- **E4 — Premier projet** : nom du projet, nom du client, taux horaire (optionnel) → [Créer]
- **E5 — « C'est prêt »** : checklist (Stockage ✓ / Mot de passe maître ✓ / Mail ✓ / Chat — / Premier projet ✓) + [Ouvrir mon espace]
- **E6 — Layout principal** : barre latérale (Aujourd'hui · Tâches · Fichiers · Messages · Notes · Temps · Facturation · Clients · ⚙ Connexions & réglages) + zone centrale

## Écrans M1

- **E7 — Aujourd'hui** : blocs « Ma journée » (tâches du jour + minuteur + RDV du jour), « Messages à traiter » (badge), « En attente d'argent », « À classer » (badge)
- **E8 — Messages** : liste unifiée (compte, expéditeur, objet, aperçu, date, 📎 si PJ)
- **E9 — Détail d'un mail** : contenu, liste des PJ, [Répondre] [Transférer]
- **E10 — Répondre** : éditeur simple, envoi depuis le compte d'origine
- **E11 — À classer** : carte par suggestion — « 📄 devis-site.pdf — reçu de marie@… par mail » + « Proposition : Projet Site web → 01_Administratif · #devis #client-marie #reçu-par-mail » + [Valider] [Modifier] [Ignorer]
- **E12 — Tâches** : liste du jour, bouton +, case à cocher en un clic
- **E13 — Connexions & réglages** : comptes connectés avec [Révoquer], stockage choisi, toggle mode avancé, rappels doux on/off

## Parcours détaillés (scénarios à tester)

- **A** : premier lancement complet (E0 → E5) en mode local sans aucun compte
- **B** : connexion Gmail par IMAP (mot de passe d'application) — succès ; puis mauvais mot de passe (message clair + aide pas à pas pour créer le mot de passe d'application) ; puis perte réseau (mode hors ligne, reprise auto à la reconnexion)
- **C** : nouveau mail avec PJ → suggestion dans « À classer » (E11) → [Valider] → le fichier passe en statut « classé » (le rangement cloud arrive en M2)
- **D** : connexion IMAP d'un FAI (ex. Orange) avec mot de passe classique
- **E** : app lancée hors ligne → données locales disponibles, synchro différée

## Règles métier M1 (moteur de suggestions)

Voir [classement-intelligent.md](classement-intelligent.md) : signaux (expéditeur, mots-clés, extension, domaine) → score 0–100 ; ≥ 80 suggestion forte, 40–79 faible, < 40 « à classer » sans proposition. **Rien n'est appliqué sans clic explicite.** Les corrections de l'utilisateur créent des règles apprises (`regle`).

## Cas d'erreur à couvrir

OAuth annulé / refusé / token révoqué (401) · réseau coupé · mauvais identifiants IMAP · PJ trop lourde (limite API) · doublon (hash SHA-256 identique) · espace cloud insuffisant (M2)

## Critères d'acceptation M0–M1

- Onboarding réalisable en < 10 min par un profil débutant (testeur externe)
- Connexion Gmail/Outlook : « C'est connecté ✓ » puis mails listés en < 30 s
- Toute PJ reçue → suggestion affichée avec dossier + étiquettes
- Aucune action sur un fichier sans clic de l'utilisateur
- Tokens chiffrés via `safeStorage`, aucun secret en clair ni dans le code
- L'app démarre et affiche les données locales hors ligne

## Hors scope M0–M1 (volontaire)

Upload vers le cloud (M2) · synchro chiffrée multi-postes (M3) · facturation · chat · notes de réunion · fiche client complète
