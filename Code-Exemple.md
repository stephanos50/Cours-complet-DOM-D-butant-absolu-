# Cours complet sur le DOM en JavaScript — de Zéro à Héros (débutant absolu)

> Ce document part **de zéro**. Chaque notion a un **exemple HTML complet** prêt à copier-coller dans un fichier `index.html`, plus un peu de JS. Ouvre `index.html` dans ton navigateur et observe le résultat.

---

## Comment utiliser les exemples

1. Crée un dossier (par ex. `dom-cours/`).
2. Crée un fichier `index.html`.
3. Copie/colle l’exemple d’une section **tel quel** dans `index.html`.
4. Ouvre le fichier dans ton navigateur (double-clique).
5. Si l’exemple contient un fichier `app.js`, crée aussi ce fichier à côté de `index.html` et colle le code JS dedans.

*(Astuce : si tu vois **`<script defer src="app.js"></script>`**, ça veut dire qu’il te faut un fichier **`app.js`**.)*

---

# Module 1 — Fondamentaux du DOM

## 1.1 Qu’est-ce que le DOM ?

**Idée** : Le navigateur transforme ton HTML en une arborescence d’objets manipulables en JS.

### Exemple HTML (afficher le titre et le body en console)

```html
<!doctype html>
<html lang="fr">
  <head>
    <meta charset="utf-8" />
    <title>DOM — Début</title>
  </head>
  <body>
    <h1>Bonjour DOM</h1>

    <script>
      console.log(document.title); // affiche le titre
      console.log(document.body);  // affiche le body (balise <body>)
    </script>
  </body>
</html>
```

## 1.2 Sélectionner des éléments

**Idée** : Récupérer un élément pour pouvoir le lire/modifier.

### Exemple HTML (plusieurs sélections)

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Sélections</title></head>
<body>
  <h1 id="titre">Titre</h1>
  <ul>
    <li class="item">Pomme</li>
    <li class="item">Poire</li>
    <li class="item">Banane</li>
  </ul>

  <script>
    const parId = document.getElementById('titre');
    const premierH1 = document.querySelector('h1');
    const tousItems = document.querySelectorAll('.item');

    console.log(parId.textContent);        // "Titre"
    console.log(premierH1 === parId);      // true
    console.log(tousItems.length);         // 3
  </script>
</body>
</html>
```

## 1.3 Parcourir l’arbre (parents, enfants, voisins)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Arbre</title></head>
<body>
  <main id="app">
    <h2>Section</h2>
    <p>Paragraphe</p>
  </main>

  <script>
    const app = document.getElementById('app');
    const h2 = app.firstElementChild;           // <h2>
    const p  = h2.nextElementSibling;           // <p>
    console.log(app.parentElement.tagName);     // BODY
    console.log(h2.textContent);                // Section
    console.log(p.previousElementSibling === h2); // true
  </script>
</body>
</html>
```

---

# Module 2 — Modifier contenu, attributs, classes, styles, dataset

## 2.1 Contenu texte vs HTML

**Idée** : `textContent` = texte brut (sécurisé). `innerHTML` = interprète du HTML (attention!).

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Contenu</title></head>
<body>
  <h1 id="t">Titre</h1>
  <div id="zone"></div>

  <script>
    const t = document.getElementById('t');
    const zone = document.getElementById('zone');

    t.textContent = 'Titre mis à jour';
    zone.textContent = '<strong>Texte</strong> (affiché en brut)';
    // Interpréter du HTML (attention aux sources non fiables)
    zone.innerHTML = '<em>Texte en italique</em>';
  </script>
</body>
</html>
```

## 2.2 Attributs

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Attributs</title></head>
<body>
  <img id="logo" src="" alt="" width="120">

  <script>
    const img = document.getElementById('logo');
    img.setAttribute('src', 'https://via.placeholder.com/120');
    img.setAttribute('alt', 'Logo de test');
    console.log(img.getAttribute('alt')); // "Logo de test"
  </script>
</body>
</html>
```

## 2.3 Classes & styles

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head>
  <meta charset="utf-8"><title>Classes & Styles</title>
  <style>
    .box { padding: 1rem; border: 2px solid; }
    .important { border-color: red; }
  </style>
</head>
<body>
  <div id="b" class="box">Boîte</div>

  <script>
    const b = document.getElementById('b');
    b.classList.add('important');     // ajoute une classe
    b.classList.toggle('important');  // enlève si présent, sinon ajoute
    b.style.backgroundColor = 'lightyellow'; // style inline
  </script>
</body>
</html>
```

## 2.4 Dataset (données personnalisées)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Dataset</title></head>
<body>
  <button id="user" data-id="42" data-role="admin">Utilisateur</button>

  <script>
    const btn = document.getElementById('user');
    console.log(btn.dataset.id);   // "42"
    console.log(btn.dataset.role); // "admin"
    btn.dataset.role = 'editor';   // changer la valeur
  </script>
</body>
</html>
```

---

# Module 3 — Créer, insérer et supprimer des éléments

## 3.1 Créer & insérer

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Créer/Insérer</title></head>
<body>
  <ul id="liste"></ul>

  <script>
    const ul = document.getElementById('liste');
    const li = document.createElement('li');
    li.textContent = 'Nouvel élément';
    ul.append(li); // ajoute à la fin
  </script>
</body>
</html>
```

## 3.2 Insertion avant/après un élément

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>before/after</title></head>
<body>
  <p id="ref">Référence</p>

  <script>
    const ref = document.getElementById('ref');
    const avant = document.createElement('div');
    avant.textContent = 'Avant';
    const apres = document.createElement('div');
    apres.textContent = 'Après';

    ref.before(avant);
    ref.after(apres);
  </script>
</body>
</html>
```

## 3.3 Supprimer

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Supprimer</title></head>
<body>
  <button id="del">Supprimer le paragraphe</button>
  <p id="p">Je vais disparaître</p>

  <script>
    document.getElementById('del').addEventListener('click', ()=>{
      document.getElementById('p').remove();
    });
  </script>
</body>
</html>
```

## 3.4 DocumentFragment (insérer beaucoup d’éléments rapidement)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Fragment</title></head>
<body>
  <ul id="list"></ul>

  <script>
    const ul = document.getElementById('list');
    const frag = document.createDocumentFragment();
    for (let i = 1; i <= 50; i++) {
      const li = document.createElement('li');
      li.textContent = 'Item ' + i;
      frag.append(li);
    }
    ul.append(frag); // une seule insertion dans le DOM
  </script>
</body>
</html>
```

---

# Module 4 — Événements (clic, clavier, délégation)

## 4.1 Clic

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Clic</title></head>
<body>
  <button id="btn">Cliquez-moi</button>

  <script>
    const btn = document.getElementById('btn');
    btn.addEventListener('click', () => {
      alert('Bouton cliqué !');
    });
  </script>
</body>
</html>
```

## 4.2 Délégation d’événements (un écouteur pour plusieurs éléments)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Délégation</title></head>
<body>
  <ul id="todos">
    <li class="todo">Tâche 1</li>
    <li class="todo">Tâche 2</li>
    <li class="todo">Tâche 3</li>
  </ul>

  <script>
    const ul = document.getElementById('todos');
    ul.addEventListener('click', (e) => {
      const li = e.target.closest('.todo');
      if (!li) return; // cliquer ailleurs ne fait rien
      li.classList.toggle('done');
    });
  </script>
  <style>.done{ text-decoration: line-through; }</style>
</body>
</html>
```

## 4.3 Clavier (touche Échap pour fermer)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Clavier</title></head>
<body>
  <div id="modal" style="border:1px solid;padding:1rem;">
    Modale ouverte — appuie sur Échap pour fermer
  </div>

  <script>
    const modal = document.getElementById('modal');
    document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') {
        modal.style.display = 'none';
      }
    });
  </script>
</body>
</html>
```

## 4.4 Empêcher un comportement par défaut (submit)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>preventDefault</title></head>
<body>
  <form id="f">
    <input name="nom" placeholder="Votre nom" required>
    <button>Envoyer</button>
  </form>
  <p id="out"></p>

  <script>
    const f = document.getElementById('f');
    const out = document.getElementById('out');
    f.addEventListener('submit', (e) => {
      e.preventDefault(); // la page ne se recharge pas
      const data = new FormData(f);
      out.textContent = 'Bonjour ' + data.get('nom') + ' !';
    });
  </script>
</body>
</html>
```

---

# Module 5 — Formulaires, validation, stockage local

## 5.1 Récupérer les données d’un formulaire

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>FormData</title></head>
<body>
  <form id="f">
    <input type="email" name="email" placeholder="Email" required>
    <input type="text" name="prenom" placeholder="Prénom" required>
    <button>Valider</button>
  </form>

  <script>
    const f = document.getElementById('f');
    f.addEventListener('submit', (e) => {
      e.preventDefault();
      const data = new FormData(f);
      const obj = Object.fromEntries(data.entries());
      console.log(obj); // { email: "...", prenom: "..." }
      alert('Merci ' + obj.prenom + ' !');
    });
  </script>
</body>
</html>
```

## 5.2 Validation personnalisée

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Validation</title></head>
<body>
  <form id="f">
    <input type="email" name="email" placeholder="Email" required>
    <span id="err" style="color:red"></span>
    <button>Envoyer</button>
  </form>

  <script>
    const f = document.getElementById('f');
    const email = f.elements.email;
    const err = document.getElementById('err');

    email.addEventListener('input', () => {
      email.setCustomValidity('');
      err.textContent = '';
      if (!email.checkValidity()) {
        email.setCustomValidity('Email invalide');
        err.textContent = 'Email invalide';
      }
    });
  </script>
</body>
</html>
```

## 5.3 Stockage local (sauvegarder automatiquement)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>localStorage</title></head>
<body>
  <form id="f">
    <input name="nom" placeholder="Votre nom">
    <button>OK</button>
  </form>

  <script>
    const KEY = 'formData';
    const f = document.getElementById('f');

    // Charger les données sauvegardées
    const saved = JSON.parse(localStorage.getItem(KEY) || '{}');
    if (saved.nom) f.elements.nom.value = saved.nom;

    // Sauvegarder à chaque frappe
    f.addEventListener('input', () => {
      const data = new FormData(f);
      localStorage.setItem(KEY, JSON.stringify(Object.fromEntries(data)));
    });
  </script>
</body>
</html>
```

---

# Module 6 — APIs modernes du DOM (Observers)

## 6.1 IntersectionObserver (lazy-load d’images)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>IntersectionObserver</title></head>
<body>
  <h2>Fais défiler la page</h2>
  <img data-src="https://via.placeholder.com/300x150?text=Image+1" alt="" style="display:block;margin:1000px 0;">
  <img data-src="https://via.placeholder.com/300x150?text=Image+2" alt="" style="display:block;margin:1000px 0;">

  <script>
    const io = new IntersectionObserver(entries => {
      for (const ent of entries) {
        if (ent.isIntersecting) {
          const img = ent.target;
          img.src = img.dataset.src; // on charge l’image quand visible
          io.unobserve(img);
        }
      }
    });

    document.querySelectorAll('img[data-src]').forEach(img => io.observe(img));
  </script>
</body>
</html>
```

## 6.2 MutationObserver (réagir aux changements du DOM)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>MutationObserver</title></head>
<body>
  <button id="add">Ajouter un item</button>
  <ul id="list"></ul>

  <script>
    const list = document.getElementById('list');
    new MutationObserver(mutations => {
      console.log('Changements :', mutations);
    }).observe(list, { childList: true });

    document.getElementById('add').addEventListener('click', () => {
      const li = document.createElement('li');
      li.textContent = 'Élément ' + (list.children.length + 1);
      list.append(li);
    });
  </script>
</body>
</html>
```

## 6.3 ResizeObserver (réagir au redimensionnement d’un élément)

### Exemple HTML

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>ResizeObserver</title></head>
<body>
  <div id="box" style="width:100px;height:100px;border:1px solid"></div>
  <button id="grow">Agrandir</button>

  <script>
    const box = document.getElementById('box');
    const btn = document.getElementById('grow');

    new ResizeObserver(entries => {
      for (const e of entries) {
        console.log('Nouvelle taille :', e.contentRect.width, 'x', e.contentRect.height);
      }
    }).observe(box);

    btn.addEventListener('click', () => {
      const w = box.offsetWidth + 20;
      const h = box.offsetHeight + 20;
      box.style.width = w + 'px';
      box.style.height = h + 'px';
    });
  </script>
</body>
</html>
```

---

# Projets pratiques (avec HTML complet)

## Projet A — To‑Do List minimaliste (ajouter/supprimer)

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>ToDo</title></head>
<body>
  <h1>Mes tâches</h1>
  <form id="todo-form">
    <input name="title" placeholder="Ajouter une tâche" required>
    <button>Ajouter</button>
  </form>
  <ul id="list"></ul>

  <script>
    const form = document.getElementById('todo-form');
    const list = document.getElementById('list');

    form.addEventListener('submit', (e) => {
      e.preventDefault();
      const fd = new FormData(form);
      const title = fd.get('title').trim();
      if (!title) return;
      const li = document.createElement('li');
      li.innerHTML = `${title} <button aria-label="Supprimer">×</button>`;
      list.append(li);
      form.reset();
    });

    list.addEventListener('click', (e) => {
      if (e.target.matches('button')) e.target.parentElement.remove();
    });
  </script>
</body>
</html>
```

## Projet B — Modale accessible (Échap pour fermer)

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Modale</title></head>
<body>
  <button id="open">Ouvrir la modale</button>

  <div id="modal" hidden role="dialog" aria-modal="true" style="position:fixed;inset:0;display:grid;place-items:center;background:#0003;">
    <div style="background:#fff;padding:1rem;min-width:240px;">
      <p>Bonjour !</p>
      <button id="close">Fermer</button>
    </div>
  </div>

  <script>
    const modal = document.getElementById('modal');
    const openBtn = document.getElementById('open');
    const closeBtn = document.getElementById('close');

    function openModal(){ modal.hidden = false; closeBtn.focus(); }
    function closeModal(){ modal.hidden = true; openBtn.focus(); }

    openBtn.addEventListener('click', openModal);
    closeBtn.addEventListener('click', closeModal);
    document.addEventListener('keydown', e => { if (e.key==='Escape') closeModal(); });
    modal.addEventListener('click', e => { if (e.target === modal) closeModal(); });
  </script>
</body>
</html>
```

## Projet C — Galerie avec lazy‑load & lightbox simple

```html
<!doctype html>
<html lang="fr">
<head><meta charset="utf-8"><title>Galerie</title></head>
<body>
  <ul id="g"></ul>
  <div id="lightbox" hidden style="position:fixed;inset:0;background:#000a;display:grid;place-items:center;">
    <img alt="" id="full" style="max-width:90vw;max-height:90vh;">
  </div>

  <script>
    // Générer des vignettes
    const g = document.getElementById('g');
    for (let i=1;i<=6;i++){
      const li = document.createElement('li');
      li.innerHTML = `<img data-src="https://via.placeholder.com/160x100?text=${i}" alt="Image ${i}" data-full="https://via.placeholder.com/800x500?text=Grande+${i}">`;
      g.append(li);
    }

    // Lazy-load
    const io = new IntersectionObserver(entries=>{
      for (const ent of entries){
        if (ent.isIntersecting){
          const img = ent.target; img.src = img.dataset.src; io.unobserve(img);
        }
      }
    });
    document.querySelectorAll('#g img').forEach(img=>io.observe(img));

    // Lightbox
    const lb = document.getElementById('lightbox');
    const full = document.getElementById('full');
    g.addEventListener('click', e=>{
      const img = e.target.closest('img'); if(!img) return;
      full.src = img.dataset.full; lb.hidden = false;
    });
    lb.addEventListener('click', ()=> lb.hidden = true);
    document.addEventListener('keydown', e=>{ if(e.key==='Escape') lb.hidden = true; });
  </script>
</body>
</html>
```


---