
# 📘 Cours DOM JavaScript — *De Zéro à Héros*

Bienvenue ! Ce dépôt contient un **cours complet** et **pratique** sur la manipulation du **DOM** en JavaScript, pensé pour **débutant absolu**.
Chaque partie fournit un **exemple HTML complet** prêt à ouvrir dans le navigateur, plus des **exercices guidés** et des **mini‑projets**.

---

## 🧭 Sommaire rapide
- `Module1` → Fondamentaux du DOM (document, sélections, navigation)
- `Module2` → Contenu, attributs, classes, styles, `dataset`
- `Module3` → Créer / insérer / supprimer + `DocumentFragment`
- `Module4` → Événements (clic, clavier) + **délégation**
- `Module5` → Formulaires (`FormData`), validation, `localStorage`
- `Module6` → Observers : `IntersectionObserver`, `MutationObserver`, `ResizeObserver`
- `Projets` → 3 mini‑apps concrètes (To‑Do, Modale, Galerie)
- `Plan7Jours` → Plan d’entraînement **pas‑à‑pas** avec **corrigés**

> Astuce : chaque fichier `.html` est autonome. **Double‑clique et observe** ✨

---

## 🚀 Démarrage rapide
1. **Télécharge** le pack (`dom-cours-exemples.zip`) et **décompresse**‑le.
2. Ouvre un fichier `.html` (double‑clic) → le navigateur s’ouvre.
3. Lis le code et **modifie** quelques lignes → **recharge** la page pour voir l’effet.

Option recommandé (confort) : **VS Code + extension “Live Server”**  
- Clique droit sur un fichier `.html` → **Open with Live Server** (auto‑rechargement).

### Alternative en ligne de commande (serveur local simple)
- **macOS / Linux** : `python3 -m http.server 8000`
- **Windows** : `py -m http.server 8000`  
Puis visite `http://localhost:8000` dans ton navigateur.

---

## 📂 Arborescence
```
dom-cours/
├─ README.md                  ← ce fichier
├─ Module1/                   ← Fondamentaux (DOM, sélection, navigation)
├─ Module2/                   ← Contenu, attributs, classes, styles, dataset
├─ Module3/                   ← Créer/Insérer/Supprimer, DocumentFragment
├─ Module4/                   ← Événements + délégation
├─ Module5/                   ← Formulaires, validation, localStorage
├─ Module6/                   ← Observers (Intersection/Mutation/Resize)
├─ Projets/
│  ├─ Projet-A-Todo.html
│  ├─ Projet-B-Modale.html
│  └─ Projet-C-Galerie.html
└─ Plan7Jours/                ← Exercices quotidiens + corrigés
   ├─ J1-A.html  J1-B.html
   ├─ J2-A.html  J2-B.html
   ├─ J3-A.html  J3-B.html
   ├─ J4-A.html  J4-B.html  J4-C.html
   ├─ J5-A.html  J5-B.html  J5-C.html
   ├─ J6-A.html  J6-B.html  J6-C.html
   └─ J7-Projet-Final.html
```

---

## 🧩 Comment utiliser les modules
- **Lis** la description en haut du fichier si présente.
- **Copie‑colle** le code dans `index.html` (ou ouvre le fichier fourni).
- **Observe** la console du navigateur (F12 → *Console*) quand le script écrit des `console.log(...)`.
- **Teste** des variantes (changer texte, classes, attributs, styles, etc.).

### Points clés par module
- **Module 1** : `document`, `querySelector(All)`, `getElementById`, navigation (`parentElement`, `children`, `nextElementSibling`, etc.).
- **Module 2** : `textContent` (sécurisé) vs `innerHTML` (interprète du HTML), `setAttribute/getAttribute`, `classList`, styles inline, `dataset`.
- **Module 3** : `createElement`, `append/prepend/before/after`, `remove`, **`DocumentFragment`** pour insérer en lot.
- **Module 4** : `addEventListener`, `e.preventDefault()`, **délégation d’événements** (écouteur sur le parent), gestion clavier (Échap).
- **Module 5** : `FormData` → objet/paire clé‑valeur, **validation native + personnalisée**, **`localStorage`** (persistance).
- **Module 6** : **Observers** modernes pour réagir au **viewport** (Intersection), **mutations DOM** (Mutation), **dimensions** (Resize).

---

## 🏋️ Plan d’entraînement (7 jours)
Chaque journée ≈ **45–60 min** avec **exercices + corrigés** : ouvre les fichiers `Plan7Jours/Jx-*.html`.
- **J1** : Découverte DOM, sélection, navigation.
- **J2** : Contenu, classes, attributs.
- **J3** : Créer/insérer/supprimer efficacement.
- **J4** : Événements + délégation + clavier.
- **J5** : Formulaires, validation, persistance locale.
- **J6** : Observers (Intersection, Mutation, Resize).
- **J7** : Mini‑app “Notes” (ajout, suppression, recherche, sauvegarde).

---

## 🧪 Projets inclus
- **Projet A — To‑Do** : ajouter/supprimer des tâches (DOM + formulaires).
- **Projet B — Modale** : modale accessible, fermeture sur Échap et clic arrière‑plan.
- **Projet C — Galerie** : lazy‑load des vignettes + “lightbox” simple.

Idées d’extensions : tri, édition en ligne, animation, thème sombre, accessibilité renforcée (focus management).

---

## 📎 Versions PDF
Le pack peut être accompagné de PDF : **complet**, **allégé (sans code)**, et **magazine** (avec table des matières).  
Si tu les as téléchargés, ouvre‑les normalement avec ton lecteur PDF.

---

## 🛠️ Outils conseillés
- **Navigateur** : Chrome, Firefox, Edge ou Safari récent.
- **Éditeur** : VS Code (+ extension *Live Server*), WebStorm, etc.
- **DevTools** : Inspecteur d’éléments, onglet *Console*, *Network*, *Performance*.

---

## ❓ FAQ / Dépannage
**Je ne vois rien quand j’ouvre le fichier.**  
→ Ouvre la **Console** (F12) pour voir les messages. Vérifie que le code est bien entre `<script> ... </script>`.

**Mon image ne s’affiche pas.**  
→ Vérifie `src` et `alt`, et l’accès internet si l’image est distante (placeholder.com).

**`innerHTML` ne marche pas ?**  
→ Utilise `textContent` pour du texte pur. `innerHTML` n’interprète que du **HTML valide** (et attention aux **failles XSS** si la source est externe).

**`localStorage` ne garde rien ?**  
→ Teste dans le même navigateur/onglet. Le stockage est **par origine** (fichier/URL).

---

## ✅ Check‑list de fin de parcours
- [ ] Sélectionner/parcourir le DOM
- [ ] Modifier contenu/attributs/classes/styles
- [ ] Créer/insérer/supprimer efficacement (Fragment)
- [ ] Gérer événements (clic/clavier) + **délégation**
- [ ] Formulaires (`FormData`), validation, **localStorage**
- [ ] Utiliser les **Observers**
- [ ] Réaliser une mini‑app complète

---

## 🔒 Licence & usage
Usage libre pour **apprentissage et projets personnels**.  
Aucune garantie — exemples fournis “en l’état”.

Bon code ! 💙
