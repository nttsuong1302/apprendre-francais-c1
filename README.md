# 📒 Bloc-notes Français — vers le C1

Un **bloc-notes web** (page unique, sans serveur ni build) pour réviser le
français et préparer le **DALF C1**. Il regroupe d'un côté les **exercices
corrigés** (productions écrites, compréhensions, etc. avec le scan du sujet et
la correction du professeur) et de l'autre des **fiches de révision** (grammaire,
vocabulaire, méthodologie) classées par thème.

L'interface est entièrement en français, avec une recherche instantanée, une
navigation par onglets et un agrandissement des images au clic.

---

## 🚀 Lancer le projet

Aucune installation, aucune dépendance, aucun build. C'est du HTML/CSS/JS pur.

- **Le plus simple :** ouvrir `index.html` directement dans le navigateur
  (double-clic).
- **Recommandé** (pour éviter d'éventuelles restrictions sur le chargement local
  des images), servir le dossier avec un petit serveur statique :

  ```bash
  # Python 3
  python3 -m http.server 8000
  # puis ouvrir http://localhost:8000
  ```

---

## 🗂️ Structure du projet

| Fichier / dossier | Rôle |
| --- | --- |
| `index.html` | Toute l'interface : structure, styles (CSS intégré) et logique (JS intégré). |
| `data.js`    | Les **exercices** : `window.TOPICS`, un tableau d'objets (sujet + correction). |
| `notes.js`   | Les **fiches de révision** : `window.NOTES`, un tableau d'objets thématiques. |
| `assets/`    | Les **images scannées** (sujets, corrections du professeur) référencées par `data.js`. |

Le navigateur charge `data.js` puis `notes.js`, qui déposent leurs données dans
`window.TOPICS` / `window.NOTES`, et le script de `index.html` construit l'affichage.

---

## ✏️ Ajouter du contenu

### Un exercice (dans `data.js`)

Ajoute un objet au tableau `window.TOPICS` :

```js
{
  "group": "✍️ Productions écrites",      // titre de la catégorie dans la liste
  "title": "Titre de l'exercice",
  "type": "Production écrite",            // badge affiché en haut de la fiche
  "exercice": {
    "imgs": ["assets/sujet-1.jpg"],       // scans du sujet (optionnel)
    "html": "<p>Transcription du sujet…</p>" // texte (optionnel)
  },
  "correction": {
    "imgs": ["assets/corr-1.jpg", "assets/corr-2.jpg"] // scans de la correction
  },
  "id": "t99"                             // identifiant unique
}
```

- `exercice` et `correction` sont facultatifs : les sous-onglets s'activent
  selon ce qui est présent.
- Place les images dans `assets/` et référence-les par leur chemin relatif.

### Une fiche de révision (dans `notes.js`)

Ajoute un objet au tableau `window.NOTES` :

```js
{
  group: "📐 Grammaire",        // catégorie
  tag: "Grammaire",            // badge affiché
  title: "Titre de la fiche",
  html: `<p>Contenu de la fiche en HTML…</p>`
}
```

---

## 🧩 Fonctionnalités

- **Deux sections** : `EXERCICES` et `NOTES`, basculables depuis la barre latérale.
- **Liste groupée par thème** avec compteur de dossiers/fiches.
- **Recherche instantanée** sur le titre et le type/tag.
- **Sous-onglets Exercice / Correction** pour chaque exercice.
- **Lightbox** : clic sur un scan pour l'agrandir, `Échap` ou clic à côté pour fermer.

---

## 💬 Prompt pour (re)créer ce projet

> Le prompt ci-dessous décrit l'application telle qu'elle existe ; il permet de
> la régénérer de zéro avec un assistant de code.

```
Crée une application web d'une seule page (HTML + CSS + JavaScript pur, sans
framework, sans build, sans serveur — un simple fichier index.html que l'on
ouvre dans le navigateur) qui sert de bloc-notes de révision pour le français
niveau DALF C1.

Données :
- Les exercices viennent d'un fichier data.js qui définit window.TOPICS, un
  tableau d'objets { group, title, type, exercice:{imgs[], html}, correction:{imgs[]}, id }.
- Les fiches de révision viennent d'un fichier notes.js qui définit
  window.NOTES, un tableau d'objets { group, tag, title, html }.
- Les images scannées (sujets, corrections du professeur) sont dans un dossier
  assets/ et référencées par chemin relatif dans imgs[].

Interface (tout en français) :
- Une barre supérieure avec le titre « Bloc-notes Français — vers le C1 ».
- Une barre latérale avec deux onglets verticaux : EXERCICES et NOTES.
- Une colonne de navigation listant les éléments groupés par « group », avec un
  champ de recherche instantanée (filtre sur le titre et le type/tag) et un
  compteur d'éléments.
- Une zone de contenu principale qui affiche l'élément sélectionné :
  - Pour un exercice : deux sous-onglets « Exercice » et « Correction »,
    activés seulement si les données existent ; chaque vue montre les scans
    (images) et/ou la transcription HTML.
  - Pour une note : le badge du tag, le titre et le contenu HTML.
- Une lightbox : cliquer sur une image l'agrandit ; fermeture avec la touche
  Échap ou un clic en dehors.

Style : ambiance chaleureuse « papeterie / bois clair », coins arrondis, ombres
douces, polices Google Fonts « Mochiy Pop One » et « Zen Maru Gothic », emojis
décoratifs. Tout le CSS et le JavaScript sont intégrés dans index.html.
```

---

*Projet personnel d'apprentissage du français — objectif DALF C1 ✨*
