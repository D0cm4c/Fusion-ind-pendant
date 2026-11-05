# Onboarding — le premier lancement

Objectif : qu'un débutant soit opérationnel en quelques minutes, sans jamais être bloqué. Chaque étape peut être sautée (« Plus tard ») et reprise ensuite depuis la checklist d'accueil.

## Parcours étape par étape (une seule question par écran)

1. **Bienvenue** — en trois phrases, ce que fait l'application (le flux recevoir → classer → suivre le temps → facturer → être payé) et la promesse « rien ne bouge sans votre validation »
2. **Où stocker vos fichiers ?**
   - *Cloud classique :*
     - [Google Drive] — connexion OAuth guidée
     - [Dropbox] — connexion OAuth guidée
   - *Cloud respectueux de la vie privée (recommandés) :*
     - [kDrive — Infomaniak] — Suisse, 15 Go gratuits, hébergement souverain
     - [pCloud] — Suisse, 10 Go gratuits
     - [MEGA] — 20 Go gratuits, chiffrement de bout en bout natif
     - [Proton Drive] — Suisse, 5 Go gratuits, zero-knowledge
     - [Nextcloud / autre cloud compatible WebDAV] — auto-hébergé ou hébergeur de confiance (Zaclys, Hetzner…)
   - [Un dossier de mon ordinateur] — mode **100 % local** : aucun compte cloud requis, les fichiers restent sur la machine (dossier au choix, emplacement proposé par défaut)
   - [Plus tard]
   - dans tous les cas cloud, la base de l'app est **chiffrée localement avant tout envoi** (voir étape mot de passe maître), donc même Google Drive devient sûr pour les données
   - si Drive ou Dropbox est choisi, étape suivante : **créer un mot de passe maître** (il chiffre la base avant synchro sur le cloud ; il ne quitte jamais l'ordinateur — une phrase de récupération imprimable est proposée). Voir [synchro-chiffree.md](synchro-chiffree.md)
3. **Quelle boîte mail connecter ?**
   - [Gmail] — OAuth guidé (Gmail API)
   - [Outlook / Microsoft 365] — OAuth guidé (Microsoft Graph)
   - [Une autre adresse mail] — **IMAP/SMTP** : détection automatique des serveurs à partir de l'adresse mail (Orange, Free, SFR, Bouygues, La Poste, OVH, Infomaniak, Yahoo, iCloud, Zoho selon plan…), ou saisie guidée étape par étape ; quand le fournisseur l'exige, le **mot de passe d'application** est expliqué en langage clair
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
