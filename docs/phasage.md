# Phasage

M1 + M2 + M3 forment le flux principal de l'application : recevoir → classer → suivre le temps → facturer → être payé.

- **M0** — Squelette Electron + onboarding guidé (choix stockage Drive / Dropbox / local, choix messagerie Gmail / Outlook / autre IMAP, chat optionnel, premier projet — voir [onboarding.md](onboarding.md)), base SQLite, tokens chiffrés via safeStorage
- **M1** — Boîte mail unifiée (Gmail + Outlook) + détection des pièces jointes + moteur de suggestions (propositions uniquement, sans upload automatique)
- **M2** — Connexion Google Drive / Dropbox + application des rangements validés (upload, arborescence `Fusion/`) + vues, filtres, doublons, corbeille, apprentissage des corrections + fils de commentaires sur chaque fichier
- **M3** — Suivi du temps (minuteur par tâche/projet, timesheet) + notes de réunion (minuteur intégré, compte-rendu, actions à faire) + facturation (devis/factures PDF générés depuis le temps passé × taux horaire, envoi par mail, suivi des paiements, TVA)
- **M4** — Chat (Telegram, Discord, lien `wa.me`) + WhatsApp Business Cloud API en module avancé optionnel

Chaque étape se termine par un test manuel guidé avec un profil « débutant » (personne n'ayant jamais configuré d'API).
