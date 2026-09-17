# Cartes de visite dynamique - GRAFFEUILLE

Toutes les cartes, un seul dépôt :

Attention pour le lien QR : 

- Ne pas renommez le nom d'utilisateur GitHub.
- Ne pas renommez le nom de votre dépôt GitHub.
- Ne passez pas le dépôt de "Public" à "Privé" (les pages GitHub gratuites doivent obligatoirement rester publiques).

| Page | À qui elle s'adresse |
| --- | --- |
| `equipe/<personne>/` | **La carte en ligne**, une adresse par employé. C'est elle qui s'ouvre quand on scanne le QR code au dos de la carte imprimée. Elle ne montre que les coordonnées, sur une page pensée pour un téléphone. |
| `index.html` | Entrée de secours : affiche la personne désignée par le fragment d'URL. |
| `editeur.html` | **L'éditeur.** On y saisit les coordonnées, on voit la carte se composer, on exporte le fichier d'impression. Aucune page publique n'y renvoie. |

Pourquoi GitHub ? : tout tourne dans le navigateur : pas de serveur, pas de compte, pas de
dépendance externe.

## Les adresses en ligne

Le site est publié à la racine du dépôt, depuis la branche `main` :

<https://roseimprimerie-dot.github.io/CDV/>


### Une adresse par employé

Ce sont celles-ci que les QR code vont ouvrir :

| Personne | Adresse |
| --- | --- |
| Alain GRAFFEUILLE | <https://roseimprimerie-dot.github.io/CDV/equipe/alain-graffeuille/> |
| Jérôme GOUMARD | <https://roseimprimerie-dot.github.io/CDV/equipe/jerome-goumard/> |
| Marie-Noëlle GRAFFEUILLE | <https://roseimprimerie-dot.github.io/CDV/equipe/marie-noelle-graffeuille/> |
| Sarah FOSSARD | <https://roseimprimerie-dot.github.io/CDV/equipe/sarah-fossard/> |
| Michaël MANCIA | <https://roseimprimerie-dot.github.io/CDV/equipe/michael-mancia/> |
| Mickaël MOREL | <https://roseimprimerie-dot.github.io/CDV/equipe/mickael-morel/> |
| Fabrice PELLIZOTTI | <https://roseimprimerie-dot.github.io/CDV/equipe/fabrice-pellizotti/> |
| Jean-Michel GAISNON | <https://roseimprimerie-dot.github.io/CDV/equipe/jean-michel-gaisnon/> |
| Loïc BERNARD | <https://roseimprimerie-dot.github.io/CDV/equipe/loic-bernard/> |

### Les autres adresses

| Adresse | Ce qu'elle ouvre |
| --- | --- |
| <https://roseimprimerie-dot.github.io/CDV/editeur.html> | L'éditeur. Aucune page publique n'y renvoie : il n'est ni listé, ni protégé. |
| <https://roseimprimerie-dot.github.io/CDV/> | Entrée de secours. Sans fragment, elle affiche la carte de Jérôme Goumard. |
| <https://roseimprimerie-dot.github.io/CDV/#loic-bernard> | Ancienne forme par identifiant, toujours acceptée pour ne pas invalider un QR déjà imprimé. |
| <https://roseimprimerie-dot.github.io/CDV/equipe/sarah-fossard/carte.json> | La fiche brute d'une personne, telle que la page la lit. |

## Un dossier par personne

Chaque employé a son propre dossier, sa propre adresse et ses propres fichiers :

```
equipe/
  _modele/                 ← à dupliquer pour ajouter quelqu'un
    index.html             ← identique partout, jamais à modifier
    carte.json             ← les coordonnées
    portrait.svg           ← les fichiers propres à la personne
  jerome-goumard/
    index.html
    carte.json
```

### L'équipe déjà en place

| Dossier | Personne | Fonction | Service |
| --- | --- | --- | --- |
| `alain-graffeuille` | Alain GRAFFEUILLE | Directeur Adjoint | |
| `jerome-goumard` | Jérôme GOUMARD | Directeur | |
| `marie-noelle-graffeuille` | Marie-Noëlle GRAFFEUILLE | Chef de projets et développement | |
| `sarah-fossard` | Sarah FOSSARD | Commerciale | Grands Comptes |
| `michael-mancia` | Michaël MANCIA | Responsable commercial | Boîtes de vitesses / Ponts |
| `mickael-morel` | Mickaël MOREL | Responsable commercial | Moteurs |
| `fabrice-pellizotti` | Fabrice PELLIZOTTI | Commercial | Boîtes de vitesses / Ponts |
| `jean-michel-gaisnon` | Jean-Michel GAISNON | Responsable Atelier | Production Moteurs |
| `loic-bernard` | Loïc BERNARD | Responsable Atelier | Production Moteurs |

Le site est `www.graffeuille.fr` pour l'ensemble de l'équipe.

### Ajouter un employé

1. Dupliquer `equipe/_modele/`, le renommer `prenom-nom`.
2. Dans l'éditeur, remplir le formulaire, mettre `prenom-nom` dans
   « Identifiant de la personne », puis **Fiche pour le site** : le fichier
   `carte.json` téléchargé remplace celui du dossier.
3. Déposer éventuellement une photo dans le dossier et écrire son nom de
   fichier dans le champ « Photo du dossier ».
   Le champ `linkedin` de `carte.json` vaut déjà la page de l'entreprise.
4. Imprimer la carte : son QR pointe déjà vers la nouvelle adresse.

`index.html` ne contient que trois lignes utiles — il désigne `carte.json` et
charge le code commun. Il est donc identique dans tous les dossiers, et une
refonte de la mise en page n'oblige jamais à repasser dessus.

## Ce que voit la personne qui scanne

Le QR code ne contient pas la fiche mais **l'adresse de la page en ligne**. La
différence compte : corriger un numéro sur le site met à jour toutes les cartes
déjà distribuées, alors qu'un QR contenant une vCard fige les coordonnées dans
l'encre.

La page affiche le logo, le portrait s'il y en a un, le nom, la fonction, puis
cinq lignes tactiles : appeler, écrire, ouvrir le site, ouvrir la page
LinkedIn, ouvrir l'itinéraire. Le bouton « Ajouter à mes contacts » télécharge
la fiche `.vcf`.

### La page LinkedIn

Le champ `linkedin` vaut par défaut la page de l'entreprise, la même pour tout
le monde :

```json
"linkedin": "https://fr.linkedin.com/company/ets-graffeuille-sas"
```

Comme c'est une page d'entreprise, la ligne affiche le nom plutôt que
l'adresse : l'URL complète tient sur deux lignes, se coupe au milieu du nom, et
n'apprend rien de plus. Une personne qui aurait son propre profil peut mettre
le sien à la place — l'identifiant seul, l'adresse sans protocole ou l'URL
complète sont acceptés — et c'est alors l'adresse qui s'affiche.

Vidé, le champ ne produit aucune ligne. La page part aussi dans la fiche
`.vcf`, en `X-SOCIALPROFILE` — ce que lit Contacts sur iPhone ; Android
l'ignore sans broncher.

Étant commune à toute l'entreprise, elle est omise de la charge compacte glissée
dans l'URL tant qu'elle n'a pas été changée, comme la couleur d'accent : cela
épargne cinquante caractères au QR des cartes sans identifiant.

La ligne n'existe que sur la carte en ligne. Le verso imprimé ne la reprend
pas : son QR mène déjà à la page, et les trois lignes de contact qu'il peut
tenir sont comptées.

### Deux formes d'adresse

| Adresse | Usage |
| --- | --- |
| `…/equipe/prenom-nom/` | **La bonne.** 77 caractères : le QR tombe en version 5, ses modules mesurent **0,54 mm** imprimés, il se scanne sans effort. |
| `…/#prenom-nom` | Ancienne forme, toujours acceptée pour ne pas invalider un QR déjà imprimé. |

### Après une modification de `carte.json`

La page relit le fichier à chaque ouverture, donc en local un simple
rafraîchissement suffit. Sur GitHub Pages, le réseau de diffusion peut servir
l'ancienne version quelques minutes après le `git push` - c'est le délai de
publication.


## Organisation du code

```
equipe/<personne>/      un dossier par employé : carte.json, photo, index.html
equipe/_modele/         gabarit à dupliquer
index.html              entrée de secours, pilotée par le fragment d'URL
editeur.html            éditeur des cartes

assets/js/contact.js    modèle partagé : valeurs, vCard, encodage de l'URL
assets/js/icons.js      pictogrammes, extraits de la fonte d'icônes d'origine
assets/js/logo.js       tracés du logo, en millimètres dans le repère de la carte
assets/js/carte.js      page publique (elle construit tout le gabarit)
assets/js/card.js       rendu SVG du recto et du verso
assets/js/qrcode.js     encodeur QR autonome (ISO/IEC 18004, mode octet)
assets/js/app.js        éditeur : formulaire, annuaire, exports
assets/css/fonts.css    fontes hébergées par le site
assets/fonts/           Roboto Condensed, Inter, Archivo (SIL OFL 1.1)
assets/css/carte.css    page publique (thèmes clair et sombre)
assets/css/app.css      éditeur et règles d'impression
assets/img/             logo et symbole en SVG, réutilisables hors de la carte
```

`card.js` est le seul endroit qui décrit la mise en page imprimée : l'aperçu,
le PDF, le SVG et le PNG sortent tous du même rendu. `contact.js` est le seul
endroit qui décrit les données, partagé par les deux pages.

L'encodeur QR est écrit à la main plutôt qu'importé d'un CDN, pour que les
pages restent utilisables hors ligne et sans dépendance à surveiller. Il a été
vérifié par relecture des codes produits (29 combinaisons de niveaux L/M/Q/H et
de versions 1 à 39, toutes relues correctement), puis sur des captures du rendu
réel de la carte, avec identifiant court et avec coordonnées en URL.

## Mise en ligne

C'est fait : `Settings → Pages`, « Deploy from a branch », branche `main`,
dossier racine. Il n'y a rien à compiler. Le fichier `.nojekyll` à la racine
demande à GitHub de servir les fichiers tels quels - sans lui, tout dossier
commençant par un tiret bas, dont `equipe/_modele`, serait écarté du site.

En local :

```sh
python3 -m http.server 8000
```

`http://localhost:8000/equipe/jerome-goumard/` ouvre sa carte,
`http://localhost:8000/editeur.html` l’éditeur.
