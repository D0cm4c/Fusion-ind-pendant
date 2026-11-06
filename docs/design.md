# Design — identité visuelle

Style retenu : **sombre, contemporain, professionnel** (« l'air pro »), avec des **mécanismes accessibles** (gros boutons explicites, une seule action primaire par carte, langage clair, contraste AA).

Maquette de référence : [maquette-accueil.png](maquette-accueil.png) — écran « Aujourd'hui », 1440×900.

## Palette

| Rôle | Hex | Usage |
|---|---|---|
| Fond app | `#0D1117` | arrière-plan global (charbon) |
| Sidebar | `#11161E` | navigation latérale |
| Carte | `#161C26` | blocs de contenu |
| Bordure | `#232C3B` | séparateurs fins 1 px |
| Texte | `#E9EDF4` | titres, contenu |
| Texte secondaire | `#8A93A6` | métadonnées, dates, aide |
| Accent cuivre | `#D97E4A` | action primaire (Valider, Relancer), item actif, logo |
| Succès | `#3FB27F` | minuteur en cours, tâche cochée |
| Danger | `#E5534B` | retards de paiement, erreurs |
| Info | `#4F7CFF` | badges secondaires |
| Pilule (étiquette) | fond `#1E2735`, texte `#9FB4D8` | tags |

## Typographie

- Police système moderne sans-serif (Inter si embarquée, sinon SF Pro / Segoe UI selon l'OS)
- Tailles : titre d'écran 32, titre de carte 17, corps 15, petit 13 — **jamais sous 13 px**
- Contraste texte/fond ≥ 4,5:1 (niveau AA) partout

## Composants

- **Fenêtre** : barre de titre native ; sidebar fixe 230 px, item actif = fond `#1B2331` + barre cuivre 3 px à gauche
- **Carte** : rayon 14 px, bordure 1 px `#232C3B`, titre à gauche + badge compteur à droite
- **Boutons** : primaire = plein cuivre, texte sombre, rayon 10 px ; secondaire = contour, texte secondaire
- **Case à cocher** : 22 px ; cochée = fond cuivre + coche sombre
- **Badge** : pilule pleine accent, texte sombre
- Règle : **une seule action primaire (cuivre) par carte/écran**

## Principes d'accessibilité (mécanismes simples, apparence pro)

- Une action principale bien visible par écran ; tout le reste en secondaire
- Les états sont toujours en **couleur + texte** (jamais la couleur seule) : « en cours », « en retard de 5 jours », « à classer (4) »
- Rappels et encouragements non bloquants, désactivables dans les réglages
- Thème sombre par défaut ; thème clair prévu post-MVP
