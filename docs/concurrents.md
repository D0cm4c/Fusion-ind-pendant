# Benchmark des applications existantes (2026)

Objectif : vérifier que notre cadrage ne manque rien d'essentiel. Prix indicatifs 2026 (à revérifier avant publication), « gratuit » = offre utilisable en solo.

## Tableau comparatif par catégorie

| Application | Catégorie | Prix indicatif | Desktop installable | Couvre | Limite pour notre cible |
|---|---|---|---|---|---|
| [Notion](https://www.notion.so) | Workspace docs + tâches | gratuit perso, ~10 $/mois Plus | web + desktop | notes, bases de données, kanban, tâches | pas de mail unifié, pas de facturation, pas de classement auto de fichiers ; « page blanche » intimidante pour un débutant |
| [Obsidian](https://obsidian.md) | Base de connaissances locale | gratuit perso (Sync payant) | oui | notes Markdown reliées, backlinks, graphe | pas de projets, temps, facturation, mail ; syntaxe `[[liens]]` à apprendre |
| [ClickUp](https://clickup.com) | Tout-en-un | gratuit, ~7 €/mois Unlimited | web + desktop | tâches, docs, chat, time tracking | facturation limitée ; interface très dense pour un débutant |
| Asana / Monday / Trello / Linear / Basecamp | Gestion de projet | gratuit à ~12 €/mois | web + desktop | kanban, timeline, tâches, équipes | rien sur mail, fichiers, facturation |
| [Toggl Track](https://toggl.com/track) | Suivi du temps | gratuit (5 users), ~12 $ Pro | web + desktop + mobile | minuteur, timesheet, rapports | pas de facturation native |
| [Clockify](https://clockify.me) | Suivi du temps | gratuit illimité, ~7 € Standard | web + desktop | minuteur, rapports, facturation (payant) | pas de mail ni de classement de fichiers |
| [Harvest](https://www.getharvest.com) | Temps + facturation | ~14 $/utilisateur | web + desktop | timesheet → facture, encaissement Stripe/PayPal, dépenses | pas de notes, mail, classement auto de fichiers |
| [Bonsai (HelloBonsai)](https://hellobonsai.com) | Suite freelance tout-en-un | ~9–49 $/mois | web surtout | contrats, devis, factures, temps, portail client, signature électronique | web-only, pas de boîte mail unifiée, pas de classement auto des pièces jointes |
| HoneyBook / Dubsado / Moxie | Gestion client (créatifs) | ~29–109 $/mois | web | propositions, contrats, portail client, paiement en ligne (commission plateforme) | idem ; orienté « vente de prestations packagées » |
| [FreshBooks](https://www.freshbooks.com) / [Wave](https://www.waveapps.com) / Zoho Invoice | Facturation / compta | FreshBooks ~19 $ Lite ; Wave gratuit (frais de paiement) | web (+ app desktop) | factures, relances de paiement, dépenses/reçus, portail client, export comptable | pas de gestion de projet ni de classement de fichiers ; temps limité |
| Pennylane / Indy / Tiime (FR) | Comptabilité en ligne FR | gratuit à ~30 €/mois | web | connexion bancaire, TVA, factures, export comptable | rien sur projets/fichiers/mail |
| Thunderbird / Spark / Mailbird / eM Client / Superhuman / Missive / Front | Client mail desktop | gratuit à ~50 $ (Superhuman ~30 $/mois) | oui | boîte unifiée multi-comptes (Gmail, Outlook, IMAP), calendrier | pas relié à des projets ; aucune ne propose de ranger automatiquement les pièces jointes reçues |
| Logseq / Joplin / Capacities / Reflect / Bear | Notes reliées (PKM) | gratuit à ~10 $/mois | oui | liens, backlinks, graphe, Markdown local | rien sur le reste du flux |
| Insync / rclone + RcloneView / CloudMounter / MultCloud | Stockage cloud unifié | payant ou gratuit (rclone) | oui | agrège Drive + Dropbox + OneDrive en un dossier | pas de tags, projets, facturation |
| Google Drive / Dropbox / OneDrive (clients natifs) | Synchro fichiers | inclus dans l'abonnement | oui | synchro des fichiers | aucun classement intelligent, aucune notion de projet |

## Checklist : fonctionnalités « standard du marché » vs notre cadrage

| Fonctionnalité | Qui la fait déjà | Dans notre cadrage ? |
|---|---|---|
| Boîte mail unifiée multi-comptes (Gmail, Outlook, IMAP) | clients mail desktop | ✅ M1 |
| Classement automatique proposé des pièces jointes reçues (mail → dossier + étiquettes → validation) | **personne nativement** | ✅ M1–M2 (notre différenciation) |
| Fichiers dans Drive/Dropbox ou en local, vus depuis l'app | Insync, rclone, clients natifs | ✅ M2 + choix local à l'onboarding |
| Notes reliées, backlinks, base de connaissances | Obsidian, Logseq, Notion, Capacities | ✅ pilier 5 (liens suggérés, pas de syntaxe) |
| Minuteur + timesheet par projet | Toggl, Clockify, Harvest | ✅ M3 |
| Devis / factures PDF envoyés par mail | Bonsai, FreshBooks, Wave, Pennylane… | ✅ M3 |
| **Relances automatiques de paiement** | FreshBooks (3 rappels), Bonsai, Zoho Invoice, Wave | ⚠️ à ajouter → M3 |
| **Export comptable (CSV/PDF pour le comptable)** | FreshBooks, Pennylane, Indy, Wave | ⚠️ à ajouter → M3 |
| Tâches d'un projet (kanban/liste) + échéances | Trello, Asana, Notion, ClickUp | ⚠️ à ajouter (léger) → M2 |
| Paiement en ligne sur la facture (Stripe/PayPal) | Harvest, Bonsai, HoneyBook (commission) | ➕ plus tard (post-M4), lien de paiement d'abord |
| Signature électronique des devis/contrats | Bonsai, HoneyBook, Dubsado | ➕ plus tard |
| Portail client (voir/signer/payer) | HoneyBook, Dubsado, Bonsai, FreshBooks | ➕ plus tard |
| Dépenses & reçus (photo/OCR) | FreshBooks, Harvest, Pennylane | ➕ plus tard (M4+) |
| Multi-devises, TVA avancée | outils de compta | ➕ plus tard |
| Calendrier des échéances (factures, relances) | la plupart des SaaS | ⚠️ à ajouter → M3 (vue simple) |
| Templates de mails rapides | peu (Superhuman IA) | ➕ M4 |
| Application desktop installable, données locales, mode hors ligne | clients mail, Obsidian, Joplin | ✅ cœur de notre positionnement |
| Onboarding guidé pour débutant non technique | quasi aucun (Trello simple mais pas guidé) | ✅ cœur de notre positionnement |

## Enseignements

1. **Personne ne fait le chaînage complet** mail → pièce jointe → classement proposé → projet → temps → facture dans une app desktop guidée : c'est notre différenciation réelle, le concept est validé.
2. **Ce qu'on avait oublié et qu'on ajoute au cadrage** : relances automatiques de paiement, export comptable, tâches/échéances par projet, calendrier des échéances (tous en M2–M3).
3. **Ce qu'on ne copie pas volontairement** : l'IA générative omniprésente, les fonctions multi-utilisateurs/équipe (cible = solo), la tarification à l'utilisateur, le tout-web.
