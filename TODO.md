# TODO - Améliorations à faire sur XLauto

## Ce qui a déjà été préparé
- Le menu mobile a été rendu fonctionnel.
- Un breakpoint tablette a été ajouté dans [style.css](style.css) pour améliorer l'affichage entre 701 px et 1024 px.
- Le header, le hero, le widget de recherche, les cartes, la section pourquoi nous choisir, les témoignages et le footer ont été adaptés pour une lecture plus confortable sur tablette.
- Des animations légères en CSS ont été ajoutées pour donner un rendu plus premium.

## À améliorer dans [index.html](index.html)

### 1. Structure HTML
- Ajouter un élément principal autour du contenu pour améliorer la sémantique : `main`.
- Vérifier que chaque section a un intitulé clair et que les boutons d'action sont cohérents.
- Si vous voulez un site plus propre, remplacer certains blocs répétitifs par des composants réutilisables plus tard.

### 2. Liens et navigation
- Rendre les liens de navigation réels vers de vraies pages ou ancres internes.
- Remplacer certains boutons qui servent uniquement de visuels par des liens si nécessaire.
- Prévoir un menu mobile plus propre avec un bouton de fermeture explicite.

### 3. Accessibilité
- Ajouter des `aria-label` sur les boutons si certains libellés ne sont pas assez explicites.
- Vérifier le contraste des textes sur les fonds sombres.
- Garder l'ordre logique du contenu pour les lecteurs d'écran.

### 4. Contenu et présentation
- Ajouter un peu plus de texte autour des sections pour raconter l'histoire de la marque.
- Uniformiser les intitulés et les espaces entre les blocs.
- Réduire le nombre de répétitions dans les textes si l'objectif est un rendu plus premium.

## À améliorer dans [style.css](style.css)

### 1. Responsive tablette
- Vérifier l'affichage du header sur tablette avec une largeur réelle de 768 px et 1024 px.
- Ajuster la taille des boutons du hero si le texte est trop long.
- Faire en sorte que le widget de recherche reste bien aligné sans casser les colonnes.
- Tester si les cartes de véhicules gardent une belle proportion sur écran intermédiaire.

### 2. Responsive mobile
- Continuer à tester le menu mobile sur plusieurs tailles d'écran.
- Masquer un second élément d'interface si l'espace devient trop réduit.
- Garder un espacement plus généreux entre les boutons et les blocs de texte.
- S'assurer que le footer ne soit pas trop dense sur petit écran.

### 3. Animations et interactions
- Ajouter une transition plus douce au menu mobile lors de son ouverture.
- Animer légèrement les cartes au survol pour un effet plus premium.
- Faire ressortir les boutons CTA avec un effet plus visible sans les rendre trop agressifs.

### 4. Cohérence visuelle
- Harmoniser les espacements entre les sections.
- Vérifier les marges autour du hero, du widget de recherche et des sections suivantes.
- Ajuster la taille des titres pour éviter qu'ils paraissent trop grands ou trop petits selon la résolution.

### 5. Styles avancés
- Ajouter un état hover plus propre sur les liens de navigation.
- Créer une version plus élégante des boutons de filtre et des cartes de véhicules.
- Préparer une palette plus raffinée si vous voulez un rendu encore plus professionnel.

## À faire plus tard : JavaScript
- Ajouter un menu mobile vraiment interactif avec ouverture/fermeture.
- Permettre de changer d'onglet dans le widget de recherche.
- Créer de petites animations au scroll ou au survol.
- Ajouter des interactions sur les filtres de véhicules si vous décidez de rendre la page dynamique.

## Ordre conseillé pour progresser
1. Vérifier l'affichage sur tablette avec plusieurs largeurs.
2. Ajuster le header et le hero.
3. Affiner les sections de véhicules et de témoignages.
4. Ajouter l'accessibilité et la cohérence des textes.
5. Ensuite seulement passer au JavaScript.

