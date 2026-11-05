# Notes de réunion et commentaires

Deux outils transverses, toujours rattachés à un projet (et donc à un client). Ils s'inscrivent dans le flux principal : une réunion = du temps à comptabiliser, une action notée = une tâche à facturer.

## Prise de notes en réunion

- Une **réunion** est rattachée à un projet : date, durée, participants
- **Écran de prise de notes dédié**, pensé pour être utilisé *pendant* la réunion : grand champ de saisie, mise en forme légère (titres, listes à cocher), horodatage optionnel de chaque point (HH:MM)
- **Minuteur intégré** : on démarre l'horloge en début de réunion, elle s'ajoute automatiquement au temps du projet — plus d'heures de réunion oubliées
- **Compte-rendu structuré** en fin de réunion : décisions / actions à faire ; chaque action peut devenir une **tâche** avec une estimation de temps, qui alimente le suivi du temps puis la facturation
- Les fichiers déposés dans une note passent par le classement intelligent (rangement + étiquettes proposés comme ailleurs)
- Recherche plein texte dans toutes les notes

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
```
