# Promos — relevé hebdomadaire (sept enseignes)

Page web et fichier de données produits automatiquement.

- **`index.html`** — l'édition courante : offres classées par grande famille,
  **alimentaire d'abord** (crémerie et laitier, fruits et légumes, puis épicerie),
  droguerie et hygiène, animalerie, bébé, et **maison / loisirs / jardin en dernier**.
  Chaque ligne porte le badge de son enseigne. Deux marqueurs à connaître :
  « carte de fidélité » (le prix suppose la carte du magasin, ex. Lidl Plus) et
  « à vérifier » (mention ambiguë sur l'affichette d'origine).
- **`promos-AAAA-MM-JJ.html`** — l'édition du jour, conservée.
- **`liste-courses.json`** — le même contenu, en JSON.
- **`offres/<date>-<source>.json`** — les relevés bruts normalisés, avec la trace de la source
  et l'horodatage de récupération.

## Périmètre : liste fermée

**ALDI, Lidl, Carrefour Monéteau, Auchan Auxerre, Netto Monéteau, Grand Frais Perrigny,
Mangeons Frais Monéteau** — et rien d'autre. `MAGASINS_SUIVIS` (`edition_promos.py`) écarte
tout le reste à l'entrée. Bonial publie une quinzaine de catalogues dans l'agglomération :
un relevé qui liste une enseigne où l'on ne va pas reste du volume à lire.

**E.Leclerc** reste « si possible » : aucune source textuelle hors de la session du drive
magasin par magasin (le prospectus national n'est qu'un index d'images).

## Comment chaque enseigne est lue

| Enseigne | Source | Lecture |
| --- | --- | --- |
| ALDI | page « offres » d'aldi.fr | JSON embarqué (`OFFER_GET`), automatisable |
| Lidl, Carrefour, Auchan | prospectus Bonial | JSON du lecteur de prospectus, automatisable |
| Netto | catalogues Bonial de l'enseigne | même lecteur ; Netto n'apparaît pas dans la grille ville, on passe par sa page enseigne |
| Grand Frais | page « offres » du magasin | page rendue côté navigateur : un passage par navigateur est nécessaire |
| Mangeons Frais | affichettes de mangeonsfrais.com | **images** : transcrites une à une (tableur `out/mangeonsfrais/lectures.json`) — la page ne publie aucun texte |

## Rythme

| Jour | Ce qui se passe |
| --- | --- |
| mardi | première édition de la semaine (la vague d'offres ALDI bascule le mardi) |
| jeudi | mise à jour, puis envoi de la page par e-mail |

## Nature de la donnée

Relevé **personnel** de pages publiques, à cadence lente. Prix des *offres* publiées par les
enseignes, jamais le tarif courant du catalogue. Les mentions du type « -50 % sur le 2ᵉ » ne sont
pas des prix : elles dépendent de la quantité achetée. Une gratuité conditionnée à un montant
d'achats (ex. une mangue offerte dès 15 €) n'est pas un prix non plus : elle apparaît avec la
mention, pas avec un montant.
Aucune garantie d'exhaustivité ni de pérennité — la structure des pages sources peut changer, auquel
cas la collecte échoue explicitement au lieu de publier une édition tronquée.
Page en `noindex` (voir `robots.txt`) : usage privé, ne pas diffuser.

Codes : `projects/veille-courses` — `aldi_offres.py`, `bonial_catalogues.py`,
`grandfrais_offres.py`, `mangeonsfrais_offres.py` (collecte), `edition_promos.py` (page + JSON).
