# Notes de réunion et commentaires

Deux outils transverses, toujours rattachés à un projet (et donc à un client). Ils s'inscrivent dans le flux principal : une réunion = du temps à comptabiliser, une action notée = une tâche à facturer.

## Prise de notes en réunion

- Une **réunion** est rattachée à un projet : date, durée, participants
- **Écran de prise de notes dédié**, pensé pour être utilisé *pendant* la réunion : grand champ de saisie, mise en forme légère (titres, listes à cocher), horodatage optionnel de chaque point (HH:MM)
- **Minuteur intégré** : on démarre l'horloge en début de réunion, elle s'ajoute automatiquement au temps du projet — plus d'heures de réunion oubliées
- **Compte-rendu structuré** en fin de réunion : décisions / actions à faire ; chaque action peut devenir une **tâche** avec une estimation de temps, qui alimente le suivi du temps puis la facturation
- Les fichiers déposés dans une note passent par le classement intelligent (rangement + étiquettes proposés comme ailleurs)
- Recherche plein texte dans toutes les notes

## Notes reliées : la base de connaissances (modèle inspiré d'Obsidian)

- Les notes sont de simples fichiers **Markdown** (texte lisible partout), stockés en local et synchronisés via le Drive/Dropbox connecté — pas de format propriétaire
- **Liens entre notes** : quand une note mentionne un projet, un client ou un fichier, l'app **propose de créer le lien automatiquement** (« Relier à la fiche client Marie Durand ? » [Oui] [Non]) — pas de syntaxe `[[...]]` à apprendre pour les débutants
- **Backlinks** : dans la fiche de chaque projet / client / fichier, on voit toutes les notes qui en parlent
- **Base de connaissances du professionnel** à côté des projets : procédures, modèles de mails, réponses types, checklists — reliées aux clients et projets concernés
- Le **graphe visuel des connexions** entre notes est réservé au mode avancé

## Commentaires sur les fichiers

- Chaque fichier enregistré dans un projet possède un **fil de commentaires** (texte, auteur, date), affiché dans la fiche du fichier ; on peut modifier ou supprimer ses propres commentaires
- Même principe sur les notes de réunion
- Les commentaires vivent dans la base **locale** (SQLite) : privés, simples, disponibles hors ligne

## Modèle de données (ajouts)

```
reunion:     id, projetId, date, dureeSecondes, participants, compteRendu
note:        id, reunionId, horodatage, texte
commentaire: id, cibleType (fichier | note), cibleId, auteur, date, texte
tache:       id, projetId, reunionId (optionnel), libelle, estimationSecondes, fait
lien:        id, noteId, cibleType (note | projet | client | fichier), cibleId
```
