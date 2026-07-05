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

## Problème actuel : header transparent + classe `scrolled` qui pose problème sur mobile

Contexte : votre header est initialement transparent et vous appliquez une classe (par exemple `scrolled`) pour assombrir son arrière-plan au scroll. Sur mobile le menu hamburger ouvre une navigation mobile qui apparaît sous le header. Après un scroll, la classe `scrolled` du header modifie son rendu et *cache* la navigation mobile ouverte.

Objectif : documenter des solutions possibles (CSS ou JS) pour corriger ce comportement sans toucher directement aux fichiers `index.html` et `style.css` pour l'instant.

Solutions proposées (avec avantages / inconvénients) :

- Option A — Ajuster le `z-index` du menu mobile (recommandée)
	- Description : s'assurer que la nav mobile a un `z-index` supérieur au header lorsque le menu est ouvert.
	- Extrait de code CSS à ajouter (dans `style.css`) :

		.header:has(.menu-toggle-input:checked) .nav {
			display: flex;
			z-index: 110; /* plus grand que .header (100) */
		}

	- Avantages : solution CSS-only, simple, aucune logique JS, instantanée.
	- Inconvénients : si d'autres éléments utilisent des z-index supérieurs il faudra vérifier l'empilage global.

- Option B — Appliquer la même propriété `scrolled` à la nav mobile
	- Description : quand la classe `scrolled` est ajoutée au header, aussi appliquer les règles visuelles nécessaires à la nav mobile (ex : même overlay, même couleur de fond semi-transparente) pour conserver la cohérence visuelle.
	- Extrait CSS exemple :

		.header.scrolled .nav,
		.header:has(.menu-toggle-input:checked).scrolled .nav {
			background-color: rgba(0,0,0,0.6); /* ou la couleur voulue */
			z-index: 105;
		}

	- Avantages : apparence cohérente.
	- Inconvénients : peut nécessiter des ajustements supplémentaires pour le positionnement et l'accessibilité.

- Option C — Fermer automatiquement le menu mobile au scroll (JS)
	- Description : détecter l'événement `scroll` et retirer l'état ouvert du menu (décocher la checkbox ou enlever la classe) pour éviter de laisser la nav ouverte pendant le scroll.
	- Extrait JS minimal à ajouter (par exemple dans un fichier `main.js`) :

		document.addEventListener('scroll', function() {
			const menuToggle = document.getElementById('menu-toggle');
			if (menuToggle && menuToggle.checked) {
				menuToggle.checked = false;
			}
		}, { passive: true });

	- Avantages : comportement net — le menu se ferme automatiquement, pas d'empilement à gérer.
	- Inconvénients : comportement parfois gênant pour l'utilisateur qui a ouvert le menu volontairement puis a fait un scroll (mais c'est souvent souhaitable sur mobile).

Recommandation : commencer par l'Option A (ajuster le `z-index`) — c'est la plus simple et la moins intrusive. Si vous voulez un rendu visuel identique, combinez A + B. Si vous préférez forcer la fermeture du menu lors d'un scroll, choisissez C.

Fichiers concernés : `index.html` (pour la checkbox/menu), `style.css` (pour les règles CSS). Avant toute modification : faire une sauvegarde (ex: `style_backup.css`, `index_backup.html`).

Si vous validez une option, je peux appliquer la modification et tester (desktop/mobile) puis commiter la modification. Indiquez quelle option vous souhaitez choisir.

