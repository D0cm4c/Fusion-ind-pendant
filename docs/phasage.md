# Phasage

M1 + M2 + M3 forment le flux principal de l'application : recevoir → classer → suivre le temps → facturer → être payé.

- **M0** — Squelette Electron + assistant de connexion pas à pas (Gmail ou Outlook en premier), base SQLite, stockage sécurisé des tokens
- **M1** — Boîte mail unifiée (Gmail + Outlook) + détection des pièces jointes + moteur de suggestions (propositions uniquement, sans upload automatique)
- **M2** — Connexion Google Drive / Dropbox + application des rangements validés (upload, arborescence `Fusion/`) + vues, filtres, doublons, corbeille, apprentissage des corrections
- **M3** — Suivi du temps (minuteur par tâche/projet, timesheet) + facturation (devis/factures PDF générés depuis le temps passé × taux horaire, envoi par mail, suivi des paiements, TVA)
- **M4** — Chat (Telegram, Discord, lien `wa.me`) + WhatsApp Business Cloud API en module avancé optionnel

Chaque étape se termine par un test manuel guidé avec un profil « débutant » (personne n'ayant jamais configuré d'API).
