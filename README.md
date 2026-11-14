# Promos — relevé hebdomadaire (ALDI, Lidl, Carrefour, Auchan)

Page web et fichier de données produits automatiquement, une fois par semaine.

- **`index.html`** — l'édition courante : offres classées par grande famille,
  **alimentaire d'abord** (crémerie et laitier, fruits et légumes, puis épicerie),
  droguerie et hygiène, animalerie, bébé, et **maison / loisirs / jardin en dernier**.
  Chaque ligne porte le badge de son enseigne ; le badge « carte de fidélité » signale un prix
  qui suppose la carte du magasin (Lidl Plus).
- **`promos-AAAA-MM-JJ.html`** — l'édition du jour, conservée.
- **`liste-courses.json`** — le même contenu au format lisible par l'extension navigateur
  `CoursesAuto` (`magasin[]` : enseigne, référence article quand elle existe, rayon, catégorie,
  prix relevé, prix barré, prix au kilo, remise, dates, n° de page du prospectus, lien vers la
  fiche produit).
- **`offres/<date>-<source>.json`** — les relevés bruts normalisés, avec la trace de la source
  et l'horodatage de récupération.

## Périmètre : quatre enseignes, liste fermée

**ALDI, Lidl, Carrefour, Auchan** — et c'est tout. Le filtre `MAGASINS_SUIVIS`
(`edition_promos.py`) écarte tout le reste à l'entrée, sans le nommer : au dernier relevé,
411 offres hors périmètre ont été écartées avant publication. Un relevé qui liste une enseigne
où l'on ne va pas reste du volume à lire.

**E.Leclerc** : demandé « si possible » — pas possible en l'état. Aucune source textuelle hors de
la session du drive, magasin par magasin (le prospectus national n'est qu'un index d'images).
L'extension sait lire les prix Leclerc quand un onglet du drive est ouvert ; un relevé sans
navigateur, non.

## Relevé du 14/11/2026

| Source | Enseignes | Offres retenues |
| --- | --- | --- |
| Page « offres » d'aldi.fr | ALDI | 210 |
| Lecteur de prospectus Bonial | Carrefour, Lidl, Auchan | 408 |

Total : **618 offres chiffrées**.

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

Codes : `projects/veille-courses` — `aldi_offres.py`, `bonial_catalogues.py` (collecte),
`edition_promos.py` (page + JSON), `fabrique_liste.py` (appariement avec une liste d'articles).
