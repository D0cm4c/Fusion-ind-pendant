# Revue critique des specs (aspect fonctionnel)

Relecture croisée du README et des 13 documents de `docs/`, après validation du mode « zéro compte développeur ».

## Ce qui tient bien

- Le flux central (recevoir → classer → temps → facturer → être payé) est cohérent de bout en bout, ancré dans les personas et les chiffres 2026
- Le principe « rien ne bouge sans validation » est présent partout (classement, relances, corbeille)
- Le mode zéro compte développeur (IMAP/SMTP + WebDAV/local) rend le MVP réellement autonome pour l'utilisateur
- Sécurité cohérente : SQLCipher + mot de passe maître, safeStorage, `.env` gitignoré, synchro chiffrée avec détection de conflit
- Phasage réaliste, chaque étape démontrable

## Incohérences corrigées dans ce commit

1. **Label « traité » sur les mails** (`classement-intelligent.md`) : en MVP IMAP, seuls les flags (lu/drapeau) existent, pas les labels Gmail → corrigé
2. **Ajout de compte post-onboarding manquant** (`spec-fonctionnelle-m0-m1.md` E13) : on ne pouvait révoquer mais pas ajouter → bouton [+ Ajouter un compte] ajouté
3. **Source des RDV/interventions non précisée** (`ecran-accueil.md`, `phasage.md`) → saisie manuelle + import CalDAV en option
4. **Relances « automatiques »** contredisaient « rien sans validation » → mode prudent = brouillon à valider, auto en mode avancé (`phasage.md`)
5. **M1 vs M2 au clic Valider** : clarifié — M1 = fiche + cache local, rangement effectif en M2
6. **RGPD** : bouton [Effacer toutes mes données] ajouté à E13

## Oublis et points faibles restants

- **Expéditeur inconnu** : le moteur de suggestions ne dit pas quoi faire d'un mail d'un inconnu (proposer « créer un client ? » n'est pas spécifié)
- **Plusieurs comptes mail** : prévu dans le modèle, le parcours UI d'ajout est maintenant là, mais pas de scénario de test
- **Cache local des PJ en clair** : les pièces jointes téléchargées en M1 sont des données perso stockées en clair dans le cache → décider si on chiffre aussi le cache
- **Mot de passe maître uniquement si cloud** : incohérent — la base locale devrait aussi être chiffrée (recommandation : oui, toujours)
- **Facturation légale FR** : mentions obligatoires (SIRET, TVA, décennale pour artisans), numérotation séquentielle, archivage 10 ans, et **facturation électronique** (réception obligatoire dès septembre 2026 pour toutes les entreprises) ne sont pas couverts → M3 doit au moins prévoir les mentions + export ; l'e-invoicing structuré reste post-MVP
- **Chat M4** : le bot Telegram/Discord est créé **une fois par nous** (développeur), pas par l'utilisateur — à documenter pour ne pas contredire « zéro compte développeur »
- **Notifications mail** : IMAP IDLE (push) ou polling à choisir côté technique
- **Recherche dans le contenu des PJ** : hors MVP (SEARCH IMAP couvre les mails, pas les PDF)
- **Tailles/quotas** : PJ trop lourde, espace cloud insuffisant — cas d'erreur à compléter en M2

## Questions ouvertes à trancher

1. Base chiffrée (mot de passe maître) même en mode 100 % local ? (recommandé : oui)
2. Cache des pièces jointes chiffré ou non ?
3. Un seul projet actif par client, ou plusieurs en parallèle ? (le modèle permet plusieurs)
4. Étiquettes : création libre par l'utilisateur en plus de celles proposées par le moteur ?

## Recommandation

Le cadrage est solide pour démarrer le M0. Traiter les 4 questions ouvertes avant la spec M2 (elles touchent au modèle de données), et compléter la conformité facturation en M3.
