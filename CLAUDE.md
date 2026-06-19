# CLAUDE.md

Guide pour travailler sur ce dépôt.

## Le projet

« Mon air intérieur » : test interactif et 100 % anonyme évaluant la qualité de
l'air d'un logement (questionnaire, score sur 100, rapport personnalisé). Outil
de la **Fondation Green-Got**, hébergé sur GitHub Pages.

- **Tout tient dans un seul fichier** : `index.html` (HTML + CSS + JS vanilla, aucune dépendance, aucun framework).
- **Aucune donnée enregistrée** : tout se passe côté client, en mémoire. Rester léger (éco-conception, zéro requête tierce hors Google Fonts).

## Conventions de rédaction (textes visibles)

- **Pas de tirets cadratins « — » dans les textes affichés.** Utiliser une
  **virgule** (incise), des **deux-points** (explication/conséquence) ou des
  **parenthèses** (énumération) selon le sens. Les traits d'union de mots
  (Green-Got, Côtes-d'Armor…) et les URL ne sont PAS concernés.
- **Aucun emoji ni pictogramme décoratif** dans l'interface (charte « sobriété
  premium »). Pour les icônes, utiliser des SVG monochromes inline.
- **Honnêteté épistémique** : distinguer faits établis, associations observées et
  pistes de recherche ; ne jamais transformer une corrélation en preuve. Garder
  les avertissements « indicatif », « ne remplace ni une mesure ni un avis médical ».
- Wording prudent sur le radon : « orientation, pas un diagnostic » ; toujours
  renvoyer à la carte officielle commune par commune (Géorisques / IRSN).

## Architecture de `index.html`

- 4 écrans (accueil, questionnaire, calcul, rapport), bascule par `showScreen()`.
- **Scoring** (`computeScore`) : 100 points moins des pénalités pondérées par
  catégorie de signal (`WEIGHTS`). Priorités triées par `CAT_ORDER`. La première
  carte affichée porte le badge « Le réflexe n°1 pour vous » (geste le plus
  impactant pour le profil, jamais un texte par défaut).
- `QUESTIONS` (18 questions), `SECTIONS` (regroupement thématique, affichage seul),
  `SIGNALS`, `STRENGTHS`, `TIERS`, `DEPARTMENTS` + `RADON_CAT*` (potentiel radon).
- Repères `// TODO analytics` posés pour un futur suivi de complétion **anonyme**
  (jamais de donnée nominative).

## Accessibilité

Contrastes ≥ WCAG AA, navigation clavier complète (`:focus-visible`, focus amené
sur l'intitulé à chaque question), ARIA (`radiogroup`/`group`, `aria-checked`,
`role="status"` sur l'écran de calcul), cibles tactiles ≥ 44 px, lien d'évitement.
Préserver ces acquis lors de toute modification.

## Workflow

- Un commit clair par changement fonctionnel, message en français.
- Vérifier la syntaxe JS avant commit (le script est inline dans `index.html`).
