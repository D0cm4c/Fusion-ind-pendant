# Classement intelligent des fichiers

C'est la **porte d'entrée** du flux de l'application (recevoir → classer → suivre le temps → facturer → être payé), pas une fin en soi. Objectif : quand un client envoie un fichier (par mail, par chat, ou déposé manuellement), l'application **propose automatiquement de le ranger au bon endroit, avec les bonnes étiquettes** — et **n'applique jamais rien sans un clic de validation** de l'utilisateur (mode prudent par défaut). Un fichier bien classé alimente ensuite le suivi du temps et la facturation du projet concerné.

## Modèle de données (SQLite)

```
fichier:  id, nom, nomNormalise, hashSHA256, taille, mime, extension,
          source (mail | chat | upload | manuel), sourceRef (id du message d'origine),
          expediteur, projetId, clientId, tags[], cheminDistant,
          dateReception, dateClassement, statut (a_classer | classe | archive | corbeille),
          confiance (score de la suggestion)

projet:   id, nom, clientId, couleur, tauxHoraire, dossierRacine
client:   id, nom, emails[], telephone, couleur
tag:      id, libelle, couleur
regle:    id, type (expediteur | mot_cle | extension | domaine), cle, dossierCible, tags, confiance, active
commentaire: id, cibleType (fichier | note), cibleId, auteur, date, texte
```

Arborescence distante proposée sur le Drive/Dropbox :

```
Fusion/
  Projets/<NomProjet>/
    01_Administratif/   (devis, factures, contrats, CGV, acomptes)
    02_Visuels/         (images, maquettes, logos, captures)
    03_Livrables/
    04_Echanges/        (fichiers reçus, en attente de classement fin)
  Clients/<NomClient>/
  Modeles/              (modèles de devis/factures)
```

## Moteur de règles (suggestions)

À l'arrivée d'un fichier, l'app calcule un **score de confiance (0–100)** à partir de signaux :

- **expéditeur** : adresse déjà connue d'un client → client + projet actif de ce client
- **mots-clés** dans l'objet du mail et dans le nom du fichier (`facture`, `devis`, `contrat`, `brief`, `logo`, `maquette`, `cgv`, `acompte`…)
- **extension** : `pdf` → administratif ; `jpg/png/webp/svg/heic` → visuels ; `zip` → livrables ; etc.
- **domaine** de l'expéditeur, taille, date

Seuils :

- score ≥ 80 → **suggestion forte**, en tête de la « Boîte à classer »
- 40–79 → suggestion faible, à confirmer
- < 40 → statut `à_classer`, sans proposition de destination

Les étiquettes peuvent aussi être **créées librement** par l'utilisateur, en plus de celles proposées par le moteur.

## Workflow type : un client envoie un fichier par mail

1. L'app détecte la pièce jointe (Gmail API / Microsoft Graph)
2. Elle calcule la suggestion : dossier cible, étiquettes, projet, client
3. Elle affiche une **carte de confirmation en langage clair** :

   > « Marie Durand vous a envoyé **devis-site.pdf**.
   > Je propose de le ranger dans **Projet « Site web » → 01_Administratif** sur votre Google Drive,
   > et de l'étiqueter : `#devis` `#client-marie` `#reçu-par-mail` »
   >
   > [Valider] [Changer le dossier] [Changer les étiquettes] [Laisser en attente]

4. Au clic **Valider** : enregistrement en base, lien mail ↔ fichier, et marquage du mail comme traité (lu / drapeau — les labels personnalisés ne sont disponibles qu'avec les API officielles, option M2+). En M1 (sans stockage connecté), la pièce jointe est téléchargée dans le **cache local** de l'app ; le rangement effectif dans `Fusion/` (WebDAV/local) intervient en M2.
5. Chaque action est écrite dans le **journal d'activité** (« Aujourd'hui 14:02 — devis-site.pdf rangé dans Site web / 01_Administratif »)

## Apprentissage

Quand l'utilisateur corrige une suggestion (autre dossier, autres étiquettes, « ne plus proposer pour cet expéditeur »), la préférence est enregistrée comme règle (`regle`) et réutilisée : **l'app apprend de vos corrections**, par expéditeur, par mot-clé ou par extension.

## Upload manuel

Un bouton **« Ajouter un fichier »** (fiche projet / client) ouvre le sélecteur de fichiers ; les suggestions de classement (dossier + étiquettes) s'appliquent exactement comme pour une pièce jointe reçue, avec validation en un clic. Voir [fiche-client.md](fiche-client.md).

## Doublons et nommage

- **Déduplication** par hash SHA-256 : un même fichier reçu deux fois est signalé comme doublon, avec proposition de ne garder qu'un exemplaire — jamais de suppression automatique
- **Renommage optionnel standardisé** : `AAAA-MM-JJ_<Projet>_<Type>_<nom-original>.ext`

## Vues et tri dans l'app

- Vues : **Tout / À classer** (badge avec le nombre en attente) / Par projet / Par client / Par type / Images / Doublons / Corbeille
- Filtres combinables (projet × étiquette × période × source) + recherche plein texte (nom, étiquettes, expéditeur)
- Tri par date, taille, nom ; **glisser-déposer** pour reclasser à la main (l'app apprend de chaque déplacement)

## Commenter un fichier

Chaque fichier classé dans un projet possède un **fil de commentaires** (texte, auteur, date), affiché dans la fiche du fichier. Les commentaires restent en local (SQLite). Voir [docs/notes-reunions.md](docs/notes-reunions.md).

## Sécurité

- Mode prudent par défaut : aucune suggestion appliquée sans clic explicite ; le classement automatique n'existe qu'en mode avancé
- Aucune suppression automatique : corbeille locale puis distante, vidage manuel uniquement
- Les pièces jointes restent dans la boîte mail d'origine ; l'app ne modifie jamais un mail sans action de l'utilisateur
