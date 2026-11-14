# Promos — relevé hebdomadaire (toutes enseignes)

Page web et fichier de données produits automatiquement, une fois par semaine.

- **`index.html`** — l'édition courante : offres des enseignes classées par grande famille,
  **alimentaire d'abord** (crémerie et laitier, fruits et légumes, puis épicerie),
  droguerie et hygiène, animalerie, bébé, et **maison / loisirs / jardin en dernier**.
  Chaque ligne porte le badge de son enseigne ; le badge « carte de fidélité » signale un prix
  qui suppose la carte du magasin (Lidl Plus, carte Super U).
- **`promos-AAAA-MM-JJ.html`** — l'édition du jour, conservée.
- **`liste-courses.json`** — le même contenu au format lisible par l'extension navigateur
  `CoursesAuto` (`magasin[]` : enseigne, référence article quand elle existe, rayon, catégorie,
  prix relevé, prix barré, prix au kilo, remise, dates, n° de page du prospectus, lien vers la
  fiche produit).
- **`offres/<date>-<source>.json`** — les relevés bruts normalisés, avec la trace de la source
  et l'horodatage de récupération.

## Sources couvertes (relevé du 14/11/2026)

| Source | Enseignes | Offres chiffrées |
| --- | --- | --- |
| Page « offres » d'aldi.fr | ALDI | 210 |
| Lecteur de prospectus Bonial | Carrefour, Carrefour Market, Super U, Lidl, Auchan, Gamm Vert | 767 |
| Page « offres » du magasin | Grand Frais Perrigny | 52 |

Total : **1029 offres chiffrées** en une passe. Hors d'atteinte sans lecture visuelle :
Mangeons Frais (affichettes en images) et E.Leclerc (promos par magasin, côté drive).

## Rythme

| Jour | Ce qui se passe |
| --- | --- |
| mardi | première édition de la semaine (la vague d'offres ALDI bascule le mardi) |
| jeudi | mise à jour, puis envoi de la page par e-mail |

## Nature de la donnée

Relevé **personnel** de pages publiques, à cadence lente (une trentaine de requêtes par semaine).
Prix des *offres* publiées par les enseignes, jamais le tarif courant du catalogue.
Les mentions du type « -50 % sur le 2ᵉ » ne sont pas des prix : elles dépendent de la quantité.
Aucune garantie d'exhaustivité ni de pérennité — la structure des pages sources peut changer, auquel
cas la collecte échoue explicitement au lieu de publier une édition tronquée.
Page en `noindex` (voir `robots.txt`) : usage privé, ne pas diffuser.

Codes : `projects/veille-courses` — `aldi_offres.py`, `bonial_catalogues.py`,
`grandfrais_offres.py` (collecte), `edition_promos.py` (page + JSON), `fabrique_liste.py`
(appariement avec une liste d'articles).
