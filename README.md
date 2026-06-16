# XLauto

Projet HTML/CSS.

## Améliorations ajoutées
- **`style.css`**
  - Correction d’un point CSS : suppression de la propriété `content` sur `.bouton` (elle ne s’applique pas aux boutons “classiques” et n’était donc pas utile).
  - Ajout d’états UX : `:hover` et `:focus-visible` pour améliorer l’interaction clavier/souris (bouton “Nous contacter”, ainsi que les boutons “Tous les véhicules” et catégories).
  - Définition plus “propre” pour éviter un impact trop global : suppression de la règle `p{ font-weight: bold; }` remplacée par des sélecteurs ciblés (`.hero p`, `.descrip p`, `.title p`, `footer p`).
  - Ajout/sécurisation visuelle : curseur `pointer` sur les boutons cliquables.

> Le rendu global reste le même, l’objectif est surtout d’améliorer la maintenabilité et l’accessibilité.


