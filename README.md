# Cours complet DOM — Débutant absolu

Ce paquet contient des **exemples HTML complets** correspondant au cours.
Ouvrez n'importe quel fichier `.html` dans votre navigateur pour tester.

Arborescence :
- Module1 à Module6 : notions de base jusqu'aux Observers
- Projets : mini‑projets concrets
- Plan7Jours : plan d'entraînement avec exercices et corrigés


# Cours complet sur le DOM en JavaScript — de Zéro à Héros (débutant absolu)
Ce document part de zéro. Chaque notion a un exemple HTML complet prêt à copier-coller dans un fichier index.html, plus un peu de JS. Ouvre index.html dans ton navigateur et observe le résultat.

## Comment utiliser les exemples
Crée un dossier (par ex. dom-cours/).
Crée un fichier index.html.
Copie/colle l’exemple d’une section tel quel dans index.html.
Ouvre le fichier dans ton navigateur (double-clique).
Si l’exemple contient un fichier app.js, crée aussi ce fichier à côté de index.html et colle le code JS dedans.
(Astuce : si tu vois <script defer src="app.js"></script>, ça veut dire qu’il te faut un fichier app.js.)

## Module 1 — Fondamentaux du DOM

### 1.1 Qu’est-ce que le DOM ?
Idée : Le navigateur transforme ton HTML en une arborescence d’objets manipulables en JS.
Exemple HTML (afficher le titre et le body en console)

### 1.2 Sélectionner des éléments
Idée : Récupérer un élément pour pouvoir le lire/modifier.
Exemple HTML (plusieurs sélections)

 
### 1.3 Parcourir l’arbre (parents, enfants, voisins)
Exemple HTML
  

## Module 2 — Modifier contenu, attributs, classes, styles, dataset

### 2.1 Contenu texte vs HTML
Idée : textContent = texte brut (sécurisé). innerHTML = interprète du HTML (attention!).
Exemple HTML
### 2.2 Attributs
Exemple HTML
### 2.3 Classes & styles
Exemple HTML
### 2.4 Dataset (données personnalisées)
Exemple HTML


## Module 3 — Créer, insérer et supprimer des éléments
### 3.1 Créer & insérer
Exemple HTML

### 3.2 Insertion avant/après un élément
Exemple HTML

### 3.3 Supprimer
Exemple HTML

### 3.4 DocumentFragment (insérer beaucoup d’éléments rapidement)
Exemple HTML



## Module 4 — Événements (clic, clavier, délégation)
### 4.1 Clic
Exemple HTML

### 4.2 Délégation d’événements (un écouteur pour plusieurs éléments)
Exemple HTML

### 4.3 Clavier (touche Échap pour fermer)
Exemple HTML

### 4.4 Empêcher un comportement par défaut (submit)
Exemple HTML

## Module 5 — Formulaires, validation, stockage local
### 5.1 Récupérer les données d’un formulaire
Exemple HTML

### 5.2 Validation personnalisée
Exemple HTML

### 5.3 Stockage local (sauvegarder automatiquement)
Exemple HTML

## Module 6 — APIs modernes du DOM (Observers)
### 6.1 IntersectionObserver (lazy-load d’images)
Exemple HTML

### 6.2 MutationObserver (réagir aux changements du DOM)
Exemple HTML

### 6.3 ResizeObserver (réagir au redimensionnement d’un élément)
Exemple HTML


# Projets pratiques (avec HTML complet)
## Projet A — To‑Do List minimaliste (ajouter/supprimer)

## Projet B — Modale accessible (Échap pour fermer)
## Projet C — Galerie avec lazy‑load & lightbox simple


### Bonnes pratiques (simples et essentielles)
Sécurité : privilégie textContent (évite les failles). N’utilise innerHTML que si nécessaire.
Performance : insère en lot (utilise DocumentFragment), évite de modifier le DOM à chaque caractère sans besoin.
Accessibilité : utilise les balises sémantiques (<button>, <nav>, etc.), gère le focus et les libellés ARIA.
Organisation : garde le JS en bas de page ou utilise <script defer src="app.js"></script>.

### Mini‑quiz (vérifie ta compréhension)

1. Quelle est la différence entre textContent et innerHTML ?
2. Comment ajouter un nouvel élément <li> dans une liste <ul> ?
3. À quoi sert e preventDefault() sur un formulaire ?
4. Explique la délégation d’événements en une phrase.
5. Que permet IntersectionObserver dans une galerie d’images ?



