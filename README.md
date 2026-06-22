# XLauto

Projet HTML/CSS.

## Améliorations ajoutées
- **`style.css`**
  - Correction d’un point CSS : suppression de la propriété `content` sur `.bouton` (elle ne s’applique pas aux boutons “classiques” et n’était donc pas utile).
  - Ajout d’états UX : `:hover` et `:focus-visible` pour améliorer l’interaction clavier/souris (bouton “Nous contacter”, ainsi que les boutons “Tous les véhicules” et catégories).
  - Définition plus “propre” pour éviter un impact trop global : suppression de la règle `p{ font-weight: bold; }` remplacée par des sélecteurs ciblés (`.hero p`, `.descrip p`, `.title p`, `footer p`).
  - Ajout/sécurisation visuelle : curseur `pointer` sur les boutons cliquables.

> Le rendu global reste le même, l’objectif est surtout d’améliorer la maintenabilité et l’accessibilité.

---

## `grid-template-areas` : comment l’utiliser pour organiser la page

### 1) C’est quoi `grid-template-areas` ?
`grid-template-areas` sert à **définir un layout Grid** en nommant des zones. Ces noms sont ensuite affectés à des éléments via `grid-area`.

- Avantage : tu lis directement le “schéma” de la page dans le CSS.
- Idéal quand tu as une **structure de page** (header/sections/footer) à placer clairement.

**Principe :**
1. Tu crées une grille (`display: grid`) sur un conteneur.
2. Tu décris les lignes/colonnes avec des noms :
   ```css
   grid-template-areas:
     "hero hero"
     "recherche recherche"
     "service service"
     "container container"
     "footer footer";
   ```
3. Tu associes chaque élément à un nom :
   ```css
   .hero { grid-area: hero; }
   .recherche { grid-area: recherche; }
   ```

Tu peux aussi utiliser `.` pour dire “vide” dans certaines zones.

### 2) Comment adapter à TES sections ? (hero / recherche / service / container / footer)
Ta page actuelle contient :
- `header.section-hero` (avec `nav.navbar` + `section.hero` + `section.recherche`)
- `section.service`
- `section.container`
- `footer`

Pour utiliser `grid-template-areas`, le plus propre est de **créer un wrapper** autour des sections principales et d’appliquer le `display:grid` sur ce wrapper.

#### Approche recommandée : grid sur un wrapper (lisible & maintenable)
Objectif : placer visuellement les “blocs” de ta page.

**Structure HTML (exemple conceptuel)**
> L’idée est de regrouper les grandes zones :
```html
<body>
  <div class="page-grid">
    <header class="section-hero">
      ...
    </header>

    <section class="service">...</section>

    <section class="container">...</section>

    <footer>...</footer>
  </div>
</body>
```

**CSS (exemple prêt à copier)**
> Exemple avec 2 colonnes pour les écrans larges, puis une seule colonne au responsive.
```css
.page-grid {
  display: grid;
  grid-template-columns: 1fr;

  /* Schéma mobile (1 colonne) */
  grid-template-areas:
    "hero"
    "recherche"
    "service"
    "container"
    "footer";
}

/* Associer les zones aux classes */
.section-hero { grid-area: hero; }
.recherche { grid-area: recherche; }
.service { grid-area: service; }
.container { grid-area: container; }
footer { grid-area: footer; }

/* Exemple version desktop : 2 colonnes */
@media (min-width: 1024px) {
  .page-grid {
    grid-template-columns: 1fr 1fr;
    grid-template-areas:
      "hero hero"
      "recherche recherche"
      "service service"
      "container container"
      "footer footer";
  }
}
```

⚠️ Note importante : dans ton `index.html` actuel, `hero` et `recherche` sont imbriqués dans le même `header.section-hero`.
- Pour que `grid-template-areas` marche “proprement” avec des zones distinctes, tu dois soit :
  1) sortir `section.recherche` hors du header (recommandé pour la clarté),
  2) soit choisir une seule zone “header/hero+recherche” (moins fin).

### 3) Variante : grid-areas local à une section (moins de changements)
Si tu ne veux pas toucher au layout global, tu peux aussi utiliser `grid-template-areas` **à l’intérieur** d’une section.

Exemples adaptés à ta page :
- **Dans `.service`** : organiser les 4 infos (icône + description) en zones nommées.
- **Dans `.card` / liste des véhicules** : définir un placement précis si tu veux un rendu type “masonry” simple (même si, souvent, Flexbox/Grid standard suffit).

### 4) Checklist pour bien l’utiliser
- Les noms dans `grid-template-areas` doivent correspondre à `grid-area`.
- Le nombre de “colonnes” implicite (ta grille) doit être cohérent sur chaque ligne de `grid-template-areas`.
- En responsive : redéfinis `grid-template-areas` dans une media query.
- Utilise `.` pour créer des “trous” (zones vides) si nécessaire.

---

## Mini guide rapide (comment l’appliquer à coup sûr)
1. Décider si tu veux un layout global (wrapper) ou local (une section).
2. Nommer les zones : `hero`, `recherche`, `service`, `container`, `footer`.
3. Ajouter `display:grid` au bon conteneur.
4. Ajouter `grid-template-areas`.
5. Associer `grid-area` à chaque élément.
6. Tester sur mobile + desktop.

---

## Menu hamburger mobile (HTML/CSS sans JS)
Pour la version mobile, le plus simple est de garder la navigation normale sur desktop et de la cacher sur petit écran, puis d’afficher un bouton “burger” qui ouvre/ferme le menu avec le principe du `checkbox` (sans JavaScript).

### 1) HTML : ajouter le bouton et grouper les liens
```html
<nav class="navbar">
  <a href="#" class="navbar-logo-link">
    <div class="navbar-logo">
      <span class="xl">XL</span><span class="auto">auto</span>
    </div>
  </a>

  <input type="checkbox" id="menu-toggle" class="menu-toggle-input">

  <label for="menu-toggle" class="menu-toggle" aria-label="Ouvrir le menu">
    <span></span>
    <span></span>
    <span></span>
  </label>

  <div class="nav-panel">
    <ul class="navbar-link">
      <li><a href="#">Accueil</a></li>
      <li><a href="#">Nos véhicules</a></li>
      <li><a href="#">Acheter</a></li>
      <li><a href="#">Louer</a></li>
      <li><a href="#">Contact</a></li>
    </ul>

    <div class="icone">
      <div class="ico">
        <img src="image/circle-user-regular.png" alt="Compte utilisateur" width="24" height="24">
      </div>
      <div class="coeur">
        <img src="image/empire-brands-solid.png" alt="Favoris" width="24" height="24">
      </div>
      <a href="#" class="bouton">
        <img src="image/phone-solid.png" alt="Téléphone" width="20" height="20">
        Nous contacter
      </a>
    </div>
  </div>
</nav>
```

### 2) CSS : cacher le bouton sur desktop, l’afficher sur mobile
```css
.navbar {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.menu-toggle-input {
  display: none;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  gap: 0.25rem;
  cursor: pointer;
}

.menu-toggle span {
  display: block;
  width: 24px;
  height: 2px;
  background: #fff;
}

.nav-panel {
  display: flex;
  align-items: center;
  gap: 1rem;
}

@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }

  .nav-panel {
    display: none;
    width: 100%;
    flex-direction: column;
    align-items: flex-start;
    padding-top: 1rem;
  }

  .menu-toggle-input:checked ~ .nav-panel {
    display: flex;
  }

  .navbar-link {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.8rem;
  }

  .icone {
    width: 100%;
    justify-content: flex-start;
    flex-wrap: wrap;
  }
}
```

### 3) Pourquoi cette méthode est utile
- Pas besoin de JavaScript pour l’instant.
- Le bouton burger est un vrai élément HTML/CSS.
- Le menu reste lisible sur grand écran.
- On peut ensuite remplacer le `checkbox` par une fonction JS plus tard.

### 4) Petit conseil pratique
Si tu veux un rendu encore plus propre sur mobile, tu peux aussi :
- réduire la taille des liens,
- ajouter un fond sombre au panneau du menu,
- garder uniquement le logo + le burger dans la navbar.

