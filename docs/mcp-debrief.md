# Pont MCP — dicter les debriefs de réunion à l'assistant IA

Oui : un **serveur MCP (Model Context Protocol) local**, embarqué dans l'app, expose des outils que tout client IA compatible MCP peut appeler. L'utilisateur dicte son debrief dans son assistant habituel, et l'app l'enregistre (réunion + note + tâches).

## Architecture

- Le process main de l'app démarre un serveur MCP sur **127.0.0.1 uniquement**, protégé par un **token généré à l'installation** (affiché dans Réglages → « Connecter mon assistant IA », régénérable)
- **Jamais exposé sur le réseau** (pas de 0.0.0.0, pas de tunnel)
- Tools exposés (MVP du pont) :
  - `projets_lister`, `clients_lister`
  - `reunion_creer(projet, date, participants)` → id
  - `note_ajouter(reunion_id, texte)` — le debrief dicté, enregistré tel quel
  - `tache_creer(projet, libelle, echeance?)` — les actions du debrief
  - `a_classer_lister()`, `suggestion_valider(id)`
  - `temps_demarrer(projet)`, `temps_arreter()`
- Toutes les écritures passent par la base SQLCipher et sont journalisées

## Scénario : debrief dicté après un RDV

1. Dans son client IA (ex. Vibe) connecté au serveur MCP local, l'utilisateur dicte : « Debrief RDV projet Site web avec Marie aujourd'hui 14h : on valide la maquette v2. Actions : j'envoie la maquette demain, on attend le retour client. »
2. Le client appelle `reunion_creer` + `note_ajouter` + 2 × `tache_creer`
3. Côté app : la réunion apparaît dans le projet, la note dans la fiche client (backlinks), les tâches arrivent dans l'écran « Aujourd'hui » — et se synchronisent chiffrées sur l'autre poste (M3)

## Règles et limites (à respecter impérativement)

- 127.0.0.1 + token uniquement ; scopes limités (notes/tâches/réunions en écriture, **aucune suppression**, pas de lecture de mails sans tool dédié explicite), toutes les actions journalisées
- Le debrief est enregistré **tel quel** — pas de résumé automatique par défaut. Un tool `note_resumer` optionnel enverrait le texte au fournisseur IA choisi par l'utilisateur : à activer explicitement, documenté RGPD
- **L'ordinateur doit être allumé** : 127.0.0.1 n'est pas joignable depuis un téléphone. Pour dicter sur le terrain : dictée vocale sur le téléphone, puis importée à l'ouverture de l'app (app mobile + synchro : post-MVP)
- Config guidée dans l'app : copier-coller de la config JSON du serveur MCP dans le client IA

## Phasage

**M4+** (après la synchro chiffrée M3, pour que les debriefs dictés suivent sur l'autre poste). Le cœur de l'app (M0–M3) reste 100 % utilisable sans aucun client IA.
