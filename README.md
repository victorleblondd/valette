# Valette — proposition de site internet pour la commune

Proposition de site internet pour la commune de Valette (Cantal, 15400), sur le modèle du site de
[Saint-Bonnet-de-Condat](https://saint-bonnet-de-condat.fr/), publiée avec GitHub Pages :
https://victorleblondd.github.io/valette/

La commune n'a pas de site internet à ce jour. Tant que la mairie n'a pas adopté la proposition
(`proposition: true` dans `_config.yml`), chaque page affiche un bandeau « Proposition de site internet »,
le site n'est pas référencé par les moteurs de recherche et les mentions légales sont au nom de l'auteur
de la proposition.

GitHub construit le site automatiquement (Jekyll) à chaque modification de la branche `main`.
Aucune installation n'est nécessaire.

## Sources des contenus

- Les avis publiés par la mairie (septembre à novembre 2026) et l'annuaire de l'administration Service-Public : coordonnées et horaires de la mairie.
- Le Répertoire national des élus (version du 20 novembre 2026) : le conseil municipal élu le 15 mars 2026 et le délégué au conseil communautaire ; la base nationale des intercommunalités (Banatic) : les groupements dont la commune est membre.
- L'Insee (population légale 2023, répertoire Sirene pour les associations), l'annuaire de l'éducation (écoles de Valette et de Menet) et Wikipédia (géographie, histoire, patrimoine, Jacques Mallouet, château de Tautal-Bas).
- Le site de l'Auberge L'Amandine et l'office de tourisme Destination Haut Cantal (restaurants, randonnées Les Eaux vives, Les Vaches rouges et Les Hauts plateaux) et Gîtes de France (hébergements).
- Santé.fr (pharmacie), VigiEau (sécheresse, consulté le 24 novembre 2026) et la préfecture du Cantal (arrêté du 17 septembre 2026).

## Ajouter un avis « Infos & Alertes »

1. Ouvrir `_data/infos_alertes.yml` et copier le modèle (en tête du fichier) **tout en haut de la liste** :
   date, type (`alerte` ou `info`), thème (`eau`, `travaux` ou `vie`), titre, résumé, et le texte de l'avis.
2. Si l'avis est une affiche : déposer le PDF dans le dossier `documents/infos-alertes/`, nommé
   `AAAA-MM-JJ-sujet-court.pdf` (sans accents ni espaces), et indiquer son nom dans le champ `pdf`.

L'avis apparaît alors sur la page Infos & Alertes et sur l'accueil.
Une alerte récente s'affiche aussi en bandeau rouge sur l'accueil pendant 3 jours
(ou jusqu'à la date indiquée dans `bandeau_jusquau`).

**Affiche disponible en ligne (image ou PDF) :** au lieu de déposer le fichier, ajouter une ligne
`adresse  documents/infos-alertes/AAAA-MM-JJ-sujet.pdf` dans `outils/fichiers-a-recuperer.txt`.
GitHub télécharge le fichier, convertit une image en PDF A4 et l'ajoute au site
(`.github/workflows/recuperer-fichiers.yml`). Plusieurs images séparées par `|` donnent un PDF de plusieurs pages.
Les affiches où figurent des personnes restent en texte, sans PDF.

## Ajouter une séance du conseil municipal

Ouvrir `_data/elus.yml` et remplacer `seances: []` par la séance (modèle dans le fichier) : date, date affichée
et points de l'ordre du jour. Les séances suivantes s'ajoutent **en tête de la liste**. Elles apparaissent sur la
page Conseil municipal (`/conseil-municipal/#seances`).

## Ajouter un rendez-vous à l'agenda

Ouvrir `_data/agenda.yml` et ajouter le rendez-vous à sa place, dans l'ordre chronologique : date, date de fin
(facultative), date affichée, titre, détail et lieu (facultatifs). Tant que la liste est vide (`[]`), remplacer
cette ligne par le rendez-vous. Les six prochains rendez-vous s'affichent sur l'accueil (la rubrique n'apparaît
que s'il y en a), tous sur la page Vie locale ; un rendez-vous passé disparaît tout seul le lendemain.

## Ajouter un document à l'affichage légal

1. Déposer le PDF dans le dossier `documents/affichage-legal/`, nommé `AAAA-MM-JJ-sujet-court.pdf`
   (ou ajouter son adresse dans `outils/fichiers-a-recuperer.txt`).
2. Ouvrir `_data/affichage_legal.yml` et copier le modèle **en tête de la liste `documents`** :
   date de publication, type (`compte-rendu`, `deliberation`, `proces-verbal`, `convocation`,
   `arrete-municipal`, `arrete-prefectoral` ou `divers`), numéro (facultatif), titre, nom du PDF.

Les filtres par type et par année apparaissent dès le premier document. Les années proposées se règlent
dans le même fichier (`annees`) ; le filtre « Année » n'apparaît qu'à partir de deux années.

## Sécheresse

Les encadrés « Sécheresse » (pages Infos & Alertes et Vie pratique) se règlent dans `_data/secheresse.yml` :
`actif: true` avec le niveau et l'arrêté en vigueur (d'après vigieau.gouv.fr), `actif: false` quand les
restrictions sont levées (situation au 24 novembre 2026).

## Publier une version (Release)

Pour marquer une version importante, ajouter un fichier `outils/versions/vX.Y.Z.md`
(par exemple `v1.0.0.md`) : titre, commit marqué, puis les notes.
GitHub crée alors la Release correspondante (`.github/workflows/publier-version.yml`).

## Modifier les informations

| À modifier | Fichier |
|---|---|
| Adresse, téléphone, courriel, horaires de la mairie | `_data/mairie.yml` |
| Maire, adjoints, conseillers, séances du conseil | `_data/elus.yml` |
| Rendez-vous | `_data/agenda.yml` |
| Menu principal | `_data/navigation.yml` |
| Bandeau d'annonce temporaire de l'accueil (texte, dernier jour d'affichage) | `_data/annonce.yml` |
| Encadrés « Sécheresse » (afficher ou masquer, niveau, arrêté) | `_data/secheresse.yml` |
| Pages | `mairie.html`, `vie-pratique.html`, `vie-locale.html`, `decouvrir.html`… |
| Apparence | `assets/css/site.css` (augmenter le numéro `?v=` dans `_includes/head.html` à chaque changement) |
| Proposition / site adopté par la commune | `_config.yml` (`proposition`) |

## Le jour où la mairie adopte le site

1. Dans `_config.yml`, passer `proposition` à `false` (le bandeau disparaît, le site devient référençable
   et les mentions légales passent au nom de la commune).
2. Avec un nom de domaine (au nom de la mairie) : ajouter un fichier `CNAME` contenant le domaine, mettre `url`
   sur `https://le-domaine.fr` et `baseurl` sur `""`, puis configurer la zone DNS (comme pour Saint-Bonnet-de-Condat).

## Organisation

- `_layouts/` : gabarits communs des pages
- `_includes/` : éléments réutilisés (avis, agenda, horaires, icônes, dates en français)
- `assets/images/` : photos du village et de l'église, blason du Cantal
- `documents/infos-alertes/` : avis en PDF
- `documents/affichage-legal/` : documents de l'affichage légal en PDF

## Crédits

- Photographie du village de Valette : France64160, [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Village_de_Valette_(Cantal).JPG), licence CC BY-SA 4.0, image recadrée et réduite.
- Photographie du bourg et de l'église Saint-Augustin : WCOMFR, [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Valette.jpg), licence CC BY 4.0.
- Blason du Cantal : dessin de Gretaz et contributeurs (Wikimedia Commons), licence CC BY-SA 3.0, image adaptée.
