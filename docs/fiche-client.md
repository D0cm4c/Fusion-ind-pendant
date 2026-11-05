# Fiche client et tableau de bord

Chaque client a une **fiche récapitulative** avec un tableau de bord : ce qui a été fait, ce qui reste à faire, les fichiers qui viennent d'arriver, ceux qui doivent partir au client.

## Contenu de la fiche client

- Identité : nom, emails, téléphone, notes de contact
- Projets du client et taux horaire
- **Travail fait** : tâches cochées, réunions avec compte-rendu, temps passé (total et par période), factures émises / payées, fichiers envoyés (tag `envoyé`)
- **Reste à faire** : tâches ouvertes avec échéances, devis / factures en attente de paiement, relances prévues
- **Fichiers arrivés récemment** : derniers fichiers reçus (mail, chat, upload manuel) pas encore classés → rappel de les valider
- **À envoyer au client** : fichiers tagués `à-envoyer` (livrables prévus)

## Génération sans agent IA

Le tableau de bord est une **agrégation des données existantes** (tâches, fichiers + statuts/étiquettes, notes, temps, factures). Aucune IA, aucun résumé automatique : quand une donnée manque (tâche sans échéance, fichier non classé, réunion sans compte-rendu, temps non saisi), l'app l'affiche comme « à compléter ».

## Encouragements à compléter (jamais bloquants)

- **Jauge de complétude** de la fiche (« complétée à 70 % ») avec les 2–3 prochaines actions proposées
- **Rappels doux contextuels** : « 3 fichiers arrivés ne sont pas encore classés », « la réunion du 12/03 n'a pas de compte-rendu », « 2 tâches sans échéance »
- Message affiché : des visualisations et un suivi fiables demandent des données complètes
- Tout est désactivable dans les réglages ; aucune fenêtre bloquante

## Upload manuel de fichiers

- Bouton **« Ajouter un fichier »** dans la fiche projet / client : sélection de un ou plusieurs fichiers → les **mêmes suggestions de classement** s'appliquent (dossier + étiquettes proposés, comme pour une pièce jointe reçue) → validation en un clic → upload vers Drive/Dropbox (ou copie dans le dossier local) + enregistrement en base
- Tag direct possible au moment de l'upload : `à-envoyer` (le fichier apparaît alors dans « à envoyer au client » du tableau de bord)

## Modèle de données (ajouts)

```
tache:    ... + echeance
fichier:  statut = a_classer | classe | archive | corbeille ; tags incluent 'à-envoyer' / 'envoyé'
```

Le workflow de suggestion pour l'upload manuel est identique à celui d'une pièce jointe reçue : voir [classement-intelligent.md](classement-intelligent.md).
