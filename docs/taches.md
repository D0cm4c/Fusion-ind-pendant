# To-do list centrale et reliée

La to-do list est un **élément central de l'application**, au même titre que la boîte à classer : elle vit dans l'écran d'accueil « Aujourd'hui » (bloc « Mes tâches »).

## Principes

- Une tâche = une action concrète, cochable en un clic (« Envoyer le devis à Marie »)
- **Reliée à tout** : chaque tâche peut être liée à un projet, un client, un fichier, un mail, une note de réunion
- Liens **bidirectionnels** : depuis la fiche client on voit ses tâches ; depuis un fichier, les tâches qui le concernent ; depuis un mail, on crée une tâche en un clic

## Création d'une tâche (partout dans l'app)

- Bouton « + » global (ou raccourci clavier)
- Depuis un mail : « Créer une tâche depuis ce mail » (lien automatique)
- Depuis un fichier : « Envoyer ce fichier » crée une tâche liée (le fichier prend le tag `à-envoyer`)
- Depuis une note de réunion : les « actions à faire » du compte-rendu deviennent des tâches liées
- Depuis la fiche client / projet

## Vues (prêtes à l'emploi, aucune configuration)

- **Aujourd'hui** (écran d'accueil) : tâches du jour, les en retard en haut
- Toutes / Par client / Par projet / Avec échéance / Faites (historique)
- Tri par échéance, projet, date de création ; glisser-déposer pour réordonner

## Ce qu'on ne fait PAS volontairement

Pas de constructeur de tableaux de bord « from scratch » façon no-code : la cible est un débutant. Les vues ci-dessus + la fiche client jouent le rôle de tableau de bord, sans configuration.

## Modèle de données

```
tache: id, projetId, clientId, libelle, fait, echeance, ordre, creeLe,
       fichierId (optionnel), messageId (optionnel), noteId (optionnel), reunionId (optionnel)
```
