# Promos — relevé hebdomadaire (ALDI France)

Page web et fichier de données produits automatiquement, une fois par semaine.

- **`index.html`** — l'édition courante : offres ALDI France classées par grande famille,
  **alimentaire d'abord** (crémerie et laitier, fruits et légumes, puis épicerie),
  droguerie et hygiène, animalerie, et **maison / loisirs / jardin en dernier**.
- **`promos-AAAA-MM-JJ.html`** — l'édition du jour, conservée.
- **`liste-courses.json`** — le même contenu au format lisible par l'extension navigateur
  `CoursesAuto` (`magasin[]` : référence article, rayon, catégorie, prix relevé, prix barré,
  prix au kilo, remise, dates de validité, URL de la fiche produit).
- **`offres/aldi-AAAA-MM-JJ.json`** — le relevé brut normalisé (avec la trace de la source
  et l'horodatage de récupération).

## Rythme

| Jour | Ce qui se passe |
| --- | --- |
| mercredi | première édition de la semaine (nouvelle vague d'offres ALDI du mardi) |
| jeudi | mise à jour, puis envoi de la page par e-mail |

## Nature de la donnée

Relevé **personnel** de pages publiques, à cadence lente (une requête par semaine pour ALDI).
Prix des *offres* publiées par l'enseigne, jamais le tarif courant du catalogue.
Les mentions du type « -50 % sur le 2ᵉ » ne sont pas des prix : elles dépendent de la quantité.
Aucune garantie d'exhaustivité ni de pérennité — la structure des pages sources peut changer,
auquel cas la collecte échoue explicitement au lieu de publier une édition tronquée.
Page en `noindex` (voir `robots.txt`) : usage privé, ne pas diffuser.

Codes : `projects/veille-courses` (poste de travail) — `aldi_offres.py` (collecte),
`edition_promos.py` (page + JSON), `fabrique_liste.py` (appariement avec une liste d'articles).
