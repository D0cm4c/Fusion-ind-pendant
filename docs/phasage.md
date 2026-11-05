# Phasage

M1 + M2 + M3 forment le flux principal de l'application : recevoir → classer → suivre le temps → facturer → être payé.

- **M0** — Squelette Electron + onboarding guidé (choix stockage Drive / Dropbox / local, choix messagerie Gmail / Outlook / autre IMAP, chat optionnel, premier projet — voir [onboarding.md](onboarding.md)), base SQLite, tokens chiffrés via safeStorage
- **M1** — Boîte mail unifiée via **IMAP/SMTP** (détection auto des serveurs, mot de passe d'application guidé ; Outlook/Graph en option via compte développeur) + détection des pièces jointes + moteur de suggestions (propositions uniquement, sans upload automatique)
- **M2** — Stockage **WebDAV ou local** (Drive/Dropbox via API officielle en option M2+, compte développeur) + application des rangements validés (upload, arborescence `Fusion/`) + **upload manuel guidé** (« Ajouter un fichier » avec les mêmes suggestions) + vues, filtres, doublons, corbeille, apprentissage des corrections + fils de commentaires sur chaque fichier + **to-do list centrale reliée** (liens fichier/mail/note/client, vues prêtes — voir [taches.md](taches.md)) + **fiche client v1** (fichiers arrivés / à envoyer, tâches faites / à faire — voir [fiche-client.md](fiche-client.md))
- **M3** — Suivi du temps (minuteur par tâche/projet, timesheet) + notes de réunion (minuteur intégré, compte-rendu, actions à faire) + facturation (devis/factures PDF générés depuis le temps passé × taux horaire, envoi par mail, **relances automatiques de paiement**, calendrier (échéances + interventions/RDV du jour avec adresse et itinéraire), **export comptable CSV/PDF**, suivi des paiements, TVA) + **fiche client enrichie** (temps, factures, jauge de complétude et rappels doux pour compléter le tableau de bord) + **synchro multi-postes chiffrée** (SQLCipher + mot de passe maître — voir [synchro-chiffree.md](synchro-chiffree.md))
- **M4** — Chat (Telegram, Discord, lien `wa.me`) + WhatsApp Business Cloud API en module avancé optionnel

Chaque étape se termine par un test manuel guidé avec un profil « débutant » (personne n'ayant jamais configuré d'API).
