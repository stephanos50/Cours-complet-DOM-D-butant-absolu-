# Référentiel des **méthodes DOM** — définitions claires (débutant)

> Objectif : donner une **définition simple**, la **signature**, ce que ça **retourne**, **quand** l’utiliser et un **mini‑exemple** pour **chaque** méthode/propriété que tu croiseras dans ce cours.

## 1) Sélectionner et naviguer dans le DOM

### `document`
**Définition** : l’objet racine qui représente la page chargée. 
**Exemples utiles** : `document.title` (titre de l’onglet), `document.body` (balise `<body>`).
```html
<script>
console.log(document.title);
console.log(document.body);
</script>
```

### `document.getElementById(id)`
**Signature** : `getElementById(id: string) → Element | null`
**Retourne** : l’élément qui a cet `id`, sinon `null`.
**Quand l’utiliser** : tu connais l’identifiant unique de l’élément.
```html
<h1 id="t">Titre</h1>
<script>
const el = document.getElementById('t');
</script>
```

### `document.querySelector(selecteur)`
**Signature** : `querySelector(sel: string) → Element | null`
**Retourne** : **le premier** élément qui matche le sélecteur CSS.
**Quand** : tu veux un élément via un sélecteur CSS (`".classe"`, `"#id"`, `"ul > li"`).
```html
<ul><li class="item">A</li><li class="item">B</li></ul>
<script>
const premierItem = document.querySelector('.item');
</script>
```

### `document.querySelectorAll(selecteur)`
**Signature** : `querySelectorAll(sel: string) → NodeList`
**Retourne** : une **liste** (NodeList) de **tous** les éléments qui matchent.
**Note** : c’est une collection itérable (`forEach`), pas un tableau.
```html
<script>
const items = document.querySelectorAll('.item');
items.forEach(li => console.log(li.textContent));
</script>
```

### Navigation : `parentElement`, `children`, `firstElementChild`, `lastElementChild`, `previousElementSibling`, `nextElementSibling`
**Définition** : propriétés pour se déplacer dans l’arbre (parent, enfants, voisins).
```html
<main id="app"><h2>Titre</h2><p>Texte</p></main>
<script>
const app = document.getElementById('app');
const h2  = app.firstElementChild;      // <h2>
const p   = h2.nextElementSibling;      // <p>
</script>
```

### `Element.closest(selecteur)`
**Signature** : `closest(sel: string) → Element | null`
**Retourne** : **le parent le plus proche** (ou l’élément lui‑même) qui correspond au sélecteur.
**Quand** : très utile en **délégation d’événements**.
```html
<script>
ul.addEventListener('click', (e) => {
  const li = e.target.closest('li');
});
</script>
```

### `Element.matches(selecteur)`
**Signature** : `matches(sel: string) → boolean`
**Retourne** : `true` si l’élément correspond au sélecteur.
```html
<script>
if (e.target.matches('.btn')) { /* ... */ }
</script>
```

---

## 2) Contenu, attributs, classes, styles, dataset

### `textContent`
**Type** : propriété (string)
**Fait** : lit/écrit du **texte brut** (ne traite pas le HTML) → **sécurisé**.
```html
<p id="z"></p>
<script>
const z = document.getElementById('z');
z.textContent = '<strong>Salut</strong>'; // affiche les < >
</script>
```

### `innerHTML`
**Type** : propriété (string)
**Fait** : lit/écrit du **HTML interprété** (crée des balises).
**Attention** : **ne jamais** y injecter du texte utilisateur brut (risque XSS).
```html
<p id="z"></p>
<script>
document.getElementById('z').innerHTML = '<em>Salut</em>';
</script>
```

### `setAttribute(name, value)` / `getAttribute(name)` / `hasAttribute(name)` / `removeAttribute(name)`
**Fait** : lire/écrire/tester/supprimer un **attribut** HTML.
```html
<img id="logo" alt="">
<script>
const img = document.getElementById('logo');
img.setAttribute('src', 'https://via.placeholder.com/120');
console.log(img.getAttribute('alt'));
console.log(img.hasAttribute('src')); // true
img.removeAttribute('alt');
</script>
```

### `dataset`
**Type** : propriété objet pour les attributs `data-*`.
```html
<button id="user" data-id="42" data-role="admin">Utilisateur</button>
<script>
const btn = document.getElementById('user');
console.log(btn.dataset.id);   // "42"
btn.dataset.role = 'editor';   // modifie data-role
</script>
```

### `classList.add(...)`, `classList.remove(...)`, `classList.toggle(...)`, `classList.contains(...)`
**Fait** : gérer les **classes CSS** d’un élément.
```html
<div id="box"></div>
<script>
const box = document.getElementById('box');
box.classList.add('important');
box.classList.toggle('important'); // ajoute/enlève
box.classList.contains('important');
</script>
```

### `style`
**Type** : propriété (objet) → styles **inline**
```html
<p id="p">Texte</p>
<script>
document.getElementById('p').style.backgroundColor = 'lightyellow';
</script>
```

---

## 3) Créer / insérer / supprimer

### `document.createElement(tagName)`
**Signature** : `createElement(tag: string) → Element`
**Fait** : crée un élément **en mémoire** (pas encore dans le DOM).
```html
<script>
const li = document.createElement('li');
li.textContent = 'Item';
</script>
```

### `append(...)` / `prepend(...)` (sur un **parent**)
**Fait** : insère à la **fin** (`append`) ou au **début** (`prepend`).
```html
<ul id="list"></ul>
<script>
list.append(li);
</script>
```

### `before(node)` / `after(node)` (sur un **élément de référence**)
**Fait** : insérer **à côté** d’un élément donné.
```html
<p id="ref">Réf</p>
<script>
ref.before(document.createElement('hr'));
ref.after(document.createElement('hr'));
</script>
```

### `remove()`
**Fait** : supprime l’élément du DOM.
```html
<script>
li.remove();
</script>
```

### `document.createDocumentFragment()`
**Fait** : conteneur **temporaire** pour regrouper beaucoup d’insertions → **performance**.
```html
<ul id="list"></ul>
<script>
const frag = document.createDocumentFragment();
for (let i=1;i<=100;i++){ const li=document.createElement('li'); li.textContent='Item '+i; frag.append(li); }
list.append(frag); // 1 seule insertion visible
</script>
```

---

## 4) Événements (clic, clavier, formulaires)

### `addEventListener(type, handler, options?)`
**Signature** : `addEventListener(type: string, handler: (event) => void, options?: {capture?:boolean, once?:boolean, passive?:boolean})`
**Fait** : **écoute** un événement sur un élément (ex: `'click'`, `'input'`, `'keydown'`).
- `type` : nom de l’événement.
- `handler` : fonction appelée quand l’événement se produit. Reçoit l’objet `event`.
- `options.once` : si `true`, le handler s’exécute **une seule fois** puis s’enlève.
- `options.passive` : si `true`, indique que le handler **ne fera pas** `preventDefault()` (utile pour le scroll).
**Retour** : rien.
```html
<button id="btn">Clique</button>
<script>
const handler = (e) => { alert('Clique !'); };
document.getElementById('btn').addEventListener('click', handler);
</script>
```

### `removeEventListener(type, handler, options?)`
**Fait** : **retire** un écouteur ajouté. Il faut **la même** fonction `handler`.
```html
btn.removeEventListener('click', handler);
```

### L’objet `event`
**Propriétés utiles** :
- `event.target` : **où** l’utilisateur a agi (élément exact).
- `event.currentTarget` : l’élément **sur lequel** l’écouteur est posé.
- `event.key` : touche clavier (pour `keydown`/`keyup`).
- `event.preventDefault()` : empêche le comportement par défaut (ex: **rechargement** d’un formulaire).
- `event.stopPropagation()` : arrête la propagation (rarement nécessaire avec une bonne délégation).

### `preventDefault()` (dans un handler)
**Fait** : annule le comportement par défaut (soumission de formulaire, navigation d’un lien, etc.).
```html
<form id="f"><input name="nom" required><button>Envoyer</button></form>
<script>
f.addEventListener('submit', (e) => { e.preventDefault(); /* traiter sans recharger */ });
</script>
```

### Délégation d’événements (pattern)
**Idée** : mettre **un seul** écouteur sur le **parent**, puis détecter l’enfant cliqué avec `closest()`.
```html
<ul id="todos"><li class="todo">A</li><li class="todo">B</li></ul>
<script>
 todos.addEventListener('click', (e) => {
   const li = e.target.closest('.todo');
   if (!li) return;
   li.classList.toggle('done');
 });
</script>
```

---

## 5) Formulaires & validation

### `new FormData(form)`
**Signature** : `FormData(form: HTMLFormElement)`
**Fait** : lit toutes les valeurs du formulaire → paires **clé/valeur**.
**Astuce** : `Object.fromEntries(new FormData(form).entries())` → objet JS.
```html
<form id="f"><input name="prenom" required><button>OK</button></form>
<script>
const data = new FormData(f);
console.log(data.get('prenom')); // valeur du champ
</script>
```

### `input.checkValidity()` / `input.reportValidity()` / `input.setCustomValidity(message)`
**Fait** : contrôle la validité; affiche les bulles d’erreur (`reportValidity`); définit un **message personnalisé** (`setCustomValidity`).
```html
<input id="email" type="email" required>
<script>
email.setCustomValidity('');
if (!email.checkValidity()) email.setCustomValidity('Email invalide');
email.reportValidity();
</script>
```

---

## 6) Stockage local (dans le navigateur)

### `localStorage.setItem(clef, valeur)` / `getItem(clef)` / `removeItem(clef)` / `clear()`
**Fait** : stocke des **chaînes** persistantes par site.
**Astuce** : pour stocker des objets, utilise `JSON.stringify` / `JSON.parse`.
```html
<script>
localStorage.setItem('nom', 'Alice');
const nom = localStorage.getItem('nom');
localStorage.removeItem('nom');
</script>
```

---

## 7) Observers (Intersection, Mutation, Resize)

### `new IntersectionObserver(callback, options?)`
**Fait** : appelle `callback(entries)` quand des éléments observés **entrent/sortent** du viewport.
**Méthodes** : `io.observe(el)`, `io.unobserve(el)`, `io.disconnect()`.
**Options** : `{ root, rootMargin, threshold }`.
```html
<img data-src="img.jpg" alt="">
<script>
const io = new IntersectionObserver(entries => {
  for (const ent of entries) if (ent.isIntersecting) {
    ent.target.src = ent.target.dataset.src; io.unobserve(ent.target);
  }
});
io.observe(document.querySelector('img'));
</script>
```

### `new MutationObserver(callback)`
**Fait** : `callback(mutations)` quand le DOM **change**.
**Méthode** : `.observe(cible, { childList, attributes, subtree })`.
```html
<ul id="list"></ul>
<script>
new MutationObserver(muts => console.log(muts)).observe(list, { childList: true });
</script>
```

### `new ResizeObserver(callback)`
**Fait** : `callback(entries)` quand la **taille** d’un élément change.
```html
<div id="box"></div>
<script>
new ResizeObserver(es => { for (const e of es) console.log(e.contentRect.width); }).observe(box);
</script>
```

---

## 8) Petits compléments pratiques

### `NodeList.forEach(...)`
**Fait** : itérer facilement sur une `NodeList` (retournée par `querySelectorAll`).
```html
<script>
document.querySelectorAll('li').forEach((li, i) => li.textContent = 'Item ' + (i+1));
</script>
```

### `getComputedStyle(element)`
**Fait** : lire le **style calculé** (utile pour connaître la vraie couleur/taille).
```html
<script>
const cs = getComputedStyle(document.body);
console.log(cs.backgroundColor);
</script>
```

---

> 💡 **Résumé** :
> - **Sélection** : `getElementById`, `querySelector(All)`
> - **Navigation** : `parentElement`, `children`, `next/previousElementSibling`, `closest`
> - **Contenu** : `textContent` (sécurisé) vs `innerHTML` (HTML)
> - **Attributs** : `set/get/has/removeAttribute`, `dataset`
> - **Classes/Styles** : `classList.*`, `style`
> - **Créer/Insérer/Supprimer** : `createElement`, `append/prepend`, `before/after`, `remove`, `DocumentFragment`
> - **Événements** : `addEventListener` / `removeEventListener`, `preventDefault`, délégation
> - **Formulaires** : `FormData`, `checkValidity`, `setCustomValidity`
> - **Stockage** : `localStorage` (+ `JSON.stringify/parse`)
> - **Observers** : `IntersectionObserver`, `MutationObserver`, `ResizeObserver`


---

# Bonnes pratiques (simples et essentielles)

- **Sécurité** : privilégie `textContent` (évite les failles). N’utilise `innerHTML` que si nécessaire.
- **Performance** : insère en lot (utilise `DocumentFragment`), évite de modifier le DOM à chaque caractère sans besoin.
- **Accessibilité** : utilise les balises sémantiques (`<button>`, `<nav>`, etc.), gère le focus et les libellés ARIA.
- **Organisation** : garde le JS en bas de page ou utilise `<script defer src="app.js"></script>`.

---

# Mini‑quiz (vérifie ta compréhension)

1. Quelle est la différence entre `textContent` et `innerHTML` ?
2. Comment ajouter un nouvel élément `<li>` dans une liste `<ul>` ?
3. À quoi sert `e.preventDefault()` sur un formulaire ?
4. Explique la **délégation d’événements** en une phrase.
5. Que permet `IntersectionObserver` dans une galerie d’images ?

> Tu veux un **plan d’entraînement de 7 jours** avec exercices corrigés pour chaque section ? Je peux l’ajouter juste en dessous. 🚀

