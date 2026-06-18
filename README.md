# 🌿 Mon air intérieur — test interactif

Page web autonome qui évalue la qualité de l'air d'un logement à partir des habitudes
de l'utilisateur, calcule un **score sur 100** et génère un **rapport personnalisé**.
Outil de marque pour la **fondation Green-Got** (santé environnementale).

- ✅ **Un seul fichier** : [`index.html`](index.html) (HTML + CSS + JS inline, sans framework ni build).
- ✅ **100 % côté client** : aucune donnée envoyée, aucun stockage navigateur, aucun tracker.
- ✅ **Responsive & accessible** : mobile-first, navigation clavier, contrastes, `prefers-reduced-motion`.
- ✅ **Déployable tel quel** sur GitHub Pages.

## 🧪 Tester en local

Ouvrez simplement `index.html` dans un navigateur (double-clic), ou servez le dossier :

```bash
python3 -m http.server 8000
# puis ouvrir http://localhost:8000
```

## ✏️ Modifier le contenu

Tout le contenu modifiable se trouve dans le bloc `<script>` en bas de [`index.html`](index.html),
dans la section **CONFIGURATION**. Aucune autre partie du code n'a besoin d'être touchée.

| Vous voulez changer… | Objet à modifier | Détails |
|---|---|---|
| Une question, ses réponses, son ordre | `QUESTIONS` | Tableau d'objets. Options listées **de la meilleure à la pire**. `signal:` déclenche une pénalité + un conseil ; `good:` déclenche un point fort ; `multi: true` = choix multiple. |
| Le barème de points retirés | `WEIGHTS` | `strong: 15`, `medium: 8`, `context: 5`, `aggrav: 4`. |
| Le texte des conseils (fait / pourquoi / action) | `SIGNALS` | Chaque clé a `cat` (catégorie de poids) et `report: { fact, why, action }`. |
| Les messages « points forts » | `STRENGTHS` | Clé = valeur `good` d'une option. |
| Les paliers de score et leurs phrases | `TIERS` | Bornes `min` (décroissantes) + `label` + `phrase`. |

### Logique de score (résumé)

- Démarre à **100**, plancher à **0**.
- Chaque signal activé retire des points selon sa catégorie (`WEIGHTS`).
- **Aggravants** : studio + aération faible ; logement récent/étanche + ventilation faible.
- **Personne sensible** (bébé, asthme/allergie, personne âgée) : ne retire **aucun point**, mais
  affiche l'encart dédié et fait remonter les conseils prioritaires.
- Paliers : 85-100 *Très bon* · 70-84 *Bon* · 50-69 *Correct* · <50 *À surveiller*.

> Règle de ton : **jamais culpabilisant**, on commence toujours par le positif.

## ☁️ Déploiement GitHub Pages

Voir les commandes exactes dans la section « Déploiement » ci-dessous ou directement dans
l'historique du projet. Une fois Pages activé sur la branche `main` (dossier racine `/`),
le site est disponible à :

```
https://<utilisateur>.github.io/<nom-du-repo>/
```

Le fichier `.nojekyll` (vide) désactive le traitement Jekyll inutile.

---

*Cet outil est informatif. Il s'appuie sur des déclarations et ne remplace ni une mesure
instrumentale de la qualité de l'air, ni un avis médical. Pour le radon, consultez les
ressources publiques officielles de votre région.*

*Un outil proposé par la fondation Green-Got pour la santé environnementale.*
