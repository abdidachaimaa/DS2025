<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

# Donne-moi le maximum d’informations et d’analyses possibles sur la base de données « Predict Students’ Dropout and Academic Success » (UCI ML Repo ID 697) via le package ucimlrepo.

python
from ucimlrepo import fetch_ucirepo

# Récupération du jeu de données

dataset = fetch_ucirepo(id=697)

# Données (features et cibles sous forme de DataFrames)

X = dataset.data.features
y = dataset.data.targets

# Métadonnées

print("=== METADATA ===")
print(dataset.metadata)

# Information sur les variables

print("=== VARIABLES ===")
print(dataset.variables)

# Dimensions

print(f"Dimensions des features : {X.shape}")
print(f"Dimensions des cibles : {y.shape}")

# Types de variables

print("Types des features :")
print(X.dtypes)
print("Types des cibles :")
print(y.dtypes)

# Aperçu des premières lignes

print("Aperçu des features :")
print(X.head())
print("Aperçu des cibles :")
print(y.head())

# Noms des variables explicatives et cibles

print("Noms des features :", list(X.columns))
print("Noms des cibles :", list(y.columns))

# Statistiques descriptives

print("Statistiques descriptives des features :")
print(X.describe(include='all'))

# Nombre de valeurs manquantes par variable

missing_X = X.isnull().sum()
missing_y = y.isnull().sum()
print("Features - valeurs manquantes :", missing_X)
print("Cibles - valeurs manquantes :", missing_y)

# Licence, contexte, origine et citation

print("Licence :", dataset.metadata.get('license'))
print("Contexte :", dataset.metadata.get('description'))
print("Origine :", dataset.metadata.get('source'))
print("DOI :", dataset.metadata.get('doi'))

La base de données « Predict Students’ Dropout and Academic Success » (UCI ML Repo ID 697) est un jeu de données complet de 4 424 étudiants visant à anticiper le décrochage ou la réussite académique à l'université grâce à des modèles de classification supervisée. Voici une présentation détaillée et une analyse contextuelle.[^1][^2]

## Contexte et finalité

- Le jeu de données vient d’une université portugaise, compilé de plusieurs sources institutionnelles, et couvre diverses filières du supérieur (agronomie, design, gestion, etc.).[^1]
- Objectif : identifier les étudiants à risque de décrochage dès leur entrée, pour pouvoir déployer des stratégies d’accompagnement adaptées.[^1]
- Problème : classification en 3 catégories – « dropout » (décrochage), « enrolled » (encore inscrit), « graduate » (diplômé).[^3][^1]


## Structure et variables

- Type : tabulaire, 36 variables explicatives (features) + cible.
- Instances : 4424 étudiants (lignes).
- Variables couvrent :
    - Informations sociodémographiques (âge, nationalité, statut marital, niveau parental)
    - Parcours académiques (mode de candidature, filière, type d’enseignement, qualification antérieure, notes obtenues)
    - Situation et contexte familial (revenu, qualifications des parents)
    - Facteurs sociaux spéciaux (besoins éducatifs spécifiques, mobilité géographique, dette étudiante)
- Les types de variables sont : réels, entiers ou catégoriels (codés par des chiffres).
- Les exemples de variables sont : « Marital Status », « Application mode », « Previous qualifications », « Previous qualification grade », « Mother's qualification », « Father's qualification », « Nationality », etc.[^4][^1]


## Propriétés analytiques

- Pas de valeurs manquantes après pré-traitement, le dataset est propre.[^1]
- Les variables cibles permettent typiquement une analyse du risque de décrochage via des arbres, des forêts ou du boosting.[^5]
- Nombre élevé de classes pour plusieurs variables (mode de candidature, filière), ce qui nécessite souvent une encodage complémentaire lors de la modélisation.


## Usage en data science

- Tâche principale : classification supervisée pour prédire le statut final de l’étudiant (modèles utilisés : XGBoost, Random Forest, Logistic Regression).[^6][^5]
- Approche courante : split 80/20 (apprentissage/test), validation croisée recommandée face à l’important déséquilibre des classes.[^1]
- Analyses typiques :
    - Identification des facteurs de risque : variables sociodémographiques/catégorielles associées au décrochage (analyse de corrélation, importance des features).[^7]
    - Segmentation et score de prédiction pour déployer des actions ciblées (bourses, tutorat, suivi personnalisé).
    - Visualisations : heatmaps de corrélation, importance des variables, distribution des cibles.


## Métadonnées et licence

- Donné sous licence libre CC BY 4.0 : libre d’usage et de modification sous réserve de citation de la source.[^1]
- DOI pour citation académique : disponible dans les métadonnées (édition 2021, M. V. Martins et al., Trends and Applications in Information Systems and Technologies).[^1]


## Exemples de traitement Python

Ton script, combiné aux méthodes de pandas, permet rapidement :

- Un aperçu des types et des valeurs des variables.
- Une quantification du déséquilibre de classe (avec value_counts sur la cible).
- L’extraction des statistiques descriptives (moyennes, écarts, distributions).
- La détection et l’analyse des valeurs aberrantes ou extrêmes (avec describe et boxplots).


## Résumé des spécificités

| Dimension | Valeur/Commentaire |
| :-- | :-- |
| Nombre d’instances | 4424[^1][^2] |
| Nombre de variables explicatives | 36[^1] |
| Type de cible | Dropout / Enrolled / Graduate (3 classes)[^1][^3] |
| Types de données | Réel, Entier, Catégoriel |
| Origine | Université portugaise, projet SATDAP[^1] |
| Licence | CC BY 4.0 |
| Description | Facteurs sociodémographiques, académiques, contextuels |
| Prét-traitement | Propre, sans valeurs manquantes |
| Citation | M.V. Martins et al., 2021, DOI référencé[^1] |

Ce jeu de données est donc idéal pour explorer les causes du décrochage et optimiser les politiques de réussite étudiante.
<span style="display:none">[^10][^11][^12][^13][^14][^15][^8][^9]</span>

<div align="center">⁂</div>

[^1]: https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success

[^2]: https://jeca.aks.or.id/jeca/article/view/13/6

[^3]: https://www.kaggle.com/datasets/naveenkumar20bps1137/predict-students-dropout-and-academic-success

[^4]: https://www.linkedin.com/pulse/predict-students-dropout-academic-success-yusuke-uehara-cpa-mba-nprfe

[^5]: https://jeca.aks.or.id/jeca/article/view/13

[^6]: https://www.sciencedirect.com/science/article/pii/S0160791X24000228

[^7]: https://github.com/hamzaezzine/Predict-students-dropout-and-academic-success-using-machine-learning-algorithms

[^8]: https://github.com/shivamsingh96/Predict-students-dropout-and-academic-success

[^9]: https://www.kaggle.com/datasets/kapturovalexander/predict-students-dropout-from-uci

[^10]: https://archive-beta.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success

[^11]: https://www.kaggle.com/datasets/mahwiz/students-dropout-and-academic-success-dataset

[^12]: https://www.kaggle.com/datasets/thedevastator/higher-education-predictors-of-student-retention

[^13]: https://www.opendatabay.com/data/science-research/fa6df8f2-382f-493f-8a16-9bbe11ccbe4c

[^14]: https://www.semanticscholar.org/paper/Predicting-Student-Dropout-and-Academic-Success-Realinho-Machado/48d44a3d027718512c82634f634044297528f159

[^15]: https://zenodo.org/records/5777340

