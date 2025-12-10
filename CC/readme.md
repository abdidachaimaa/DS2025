# Compte Rendu - Analyse du Dataset Iris avec Random Forest

## 1. Introduction

### Descriptif de l'analyse

La base de données Iris, introduite par Ronald Fisher en 1936, constitue un benchmark classique en apprentissage automatique pour la classification supervisée multiclasse. Elle regroupe 150 échantillons mesurés sur trois espèces d'iris : Iris setosa (50 obs.), Iris versicolor (50 obs.) et Iris virginica (50 obs.).​

**Structure et Schéma**
Le dataset est organisé en une unique table relationnelle de 150 lignes et 6 colonnes :

**id** : identifiant unique entier (1 à 150).

**SepalLengthCm, SepalWidthCm** : dimensions du sépale en cm (réelles).

**PetalLengthCm, PetalWidthCm** : dimensions du pétale en cm (réelles).

**Species** : variable cible catégorielle à 3 niveaux.​

Aucune valeur manquante n'est observée, assurant une intégrité parfaite des données.

### Objectif du projet
Ce projet vise à entraîner et évaluer un modèle de classification basé sur l'algorithme **Random Forest** pour prédire l'espèce des fleurs d'Iris à partir de leurs caractéristiques morphologiques.

### Dataset utilisé
- **Source** : Dataset Iris de l'UCI Machine Learning Repository (via Kaggle)
- **Nombre d'observations** : 150 entrées
- **Nombre de variables** : 6 colonnes

---

## 2. Description des données

### Structure du dataset

Le dataset contient les colonnes suivantes :

| Colonne | Type | Description |
|---------|------|-------------|
| Id | int64 | Identifiant unique de chaque observation |
| SepalLengthCm | float64 | Longueur du sépale en centimètres |
| SepalWidthCm | float64 | Largeur du sépale en centimètres |
| PetalLengthCm | float64 | Longueur du pétale en centimètres |
| PetalWidthCm | float64 | Largeur du pétale en centimètres |
| Species | object | Espèce de la fleur d'Iris (variable cible) |

### Caractéristiques des données
- **Valeurs manquantes** : 0 (aucune valeur manquante détectée)
- **Lignes dupliquées** : 0 (aucun doublon)
- **Conclusion** : Le dataset est déjà propre et ne nécessite aucun nettoyage

### Code Python - Chargement et nettoyage

```python
import kagglehub
import pandas as pd

# Téléchargement du dataset depuis Kaggle
path = kagglehub.dataset_download("uciml/iris")
print("Path to dataset files:", path)

# Chargement du dataset
dataset = pd.read_csv(f'{path}/Iris.csv')

# Affichage des informations du dataset
print("Dataset Info:")
dataset.info()

# Vérification des valeurs manquantes
print("\nMissing Values:")
print(dataset.isnull().sum())

# Vérification des lignes dupliquées
print("\nDuplicate Rows:")
duplicate_rows = dataset.duplicated().sum()
print(duplicate_rows)

# Validation de la propreté des données
if dataset.isnull().sum().sum() == 0 and duplicate_rows == 0:
    print("\nDataset is already clean.")
```

**Résultat** : Le dataset contient 150 entrées avec 6 colonnes, aucune valeur manquante et aucun doublon.

---

## 3. Préparation des données

### Séparation des variables

**Variables explicatives (X)** :
- SepalLengthCm
- SepalWidthCm
- PetalLengthCm
- PetalWidthCm

**Variable cible (y)** :
- Species (3 classes : Iris-setosa, Iris-versicolor, Iris-virginica)

### Division du dataset

Le dataset a été divisé en deux ensembles :

| Ensemble | Taille | Proportion |
|----------|--------|------------|
| Entraînement (train) | 120 observations | 80% |
| Test | 30 observations | 20% |

**Paramètres utilisés** :
- `test_size = 0.2` (20% pour le test)
- `random_state = 42` (pour la reproductibilité des résultats)

### Code Python - Préparation

```python
from sklearn.model_selection import train_test_split

# Définition des variables explicatives (X) et de la cible (y)
X = dataset.drop(['Id', 'Species'], axis=1)
y = dataset['Species']

# Division des données en ensembles d'entraînement et de test
X_train, X_test, y_train, y_test = train_test_split(
    X, y, 
    test_size=0.2, 
    random_state=42
)

print("Shape of X_train:", X_train.shape)  # (120, 4)
print("Shape of X_test:", X_test.shape)    # (30, 4)
print("Shape of y_train:", y_train.shape)  # (120,)
print("Shape of y_test:", y_test.shape)    # (30,)
```

---

## 4. Algorithme de Machine Learning : Random Forest

### Qu'est-ce que le Random Forest ?

Le **Random Forest** (Forêt Aléatoire) est un algorithme d'apprentissage supervisé basé sur un ensemble d'arbres de décision. Il fonctionne selon les principes suivants :

1. **Construction de multiples arbres** : Création de nombreux arbres de décision indépendants
2. **Échantillonnage aléatoire** : Chaque arbre est entraîné sur un sous-ensemble aléatoire des données
3. **Sélection aléatoire des variables** : À chaque nœud, un sous-ensemble aléatoire de variables est considéré
4. **Vote majoritaire** : Pour la classification, la prédiction finale est obtenue par vote majoritaire de tous les arbres

### Avantages du Random Forest
- Résistance au surapprentissage (overfitting)
- Gestion efficace des données multidimensionnelles
- Robustesse face aux valeurs aberrantes
- Pas besoin de normalisation des données

### Paramètres du modèle

```python
RandomForestClassifier(random_state=42)
```

Le modèle utilise les paramètres par défaut de scikit-learn, avec `random_state=42` pour assurer la reproductibilité.

---

## 5. Entraînement du modèle

Le modèle Random Forest a été entraîné sur les 120 observations de l'ensemble d'entraînement. L'algorithme a appris les relations entre les caractéristiques morphologiques des fleurs et leur espèce correspondante.

**Étapes d'entraînement** :
1. Instanciation du modèle RandomForestClassifier
2. Ajustement du modèle aux données d'entraînement (X_train, y_train)
3. Construction de la forêt d'arbres de décision

### Code Python - Entraînement

```python
from sklearn.ensemble import RandomForestClassifier

# Instanciation du modèle Random Forest Classifier
model = RandomForestClassifier(random_state=42)

# Entraînement du modèle sur les données d'entraînement
model.fit(X_train, y_train)

print("Random Forest Classifier model trained successfully.")
```

**Explication du code** :
- `RandomForestClassifier(random_state=42)` : Crée un modèle avec les paramètres par défaut
- `model.fit(X_train, y_train)` : Entraîne le modèle sur les données d'entraînement
- Le paramètre `random_state=42` assure la reproductibilité des résultats

---

## 6. Évaluation du modèle

### Métriques de performance

Le modèle a été évalué sur l'ensemble de test (30 observations) avec les résultats suivants :

### Code Python - Évaluation

```python
from sklearn.metrics import accuracy_score, classification_report, confusion_matrix

# Prédictions sur l'ensemble de test
y_pred = model.predict(X_test)

# Calcul de la précision globale (Accuracy)
accuracy = accuracy_score(y_test, y_pred)
print(f"\nAccuracy: {accuracy:.4f}")

# Affichage du rapport de classification détaillé
print("\nClassification Report:")
print(classification_report(y_test, y_pred))

# Affichage de la matrice de confusion
print("\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred))
```

#### Accuracy (Précision globale)
**Accuracy = 1.0000 (100%)**

Le modèle a correctement classifié toutes les fleurs d'Iris de l'ensemble de test.

#### Rapport de classification détaillé

| Espèce | Precision | Recall | F1-Score | Support |
|--------|-----------|--------|----------|---------|
| Iris-setosa | 1.00 | 1.00 | 1.00 | 10 |
| Iris-versicolor | 1.00 | 1.00 | 1.00 | 9 |
| Iris-virginica | 1.00 | 1.00 | 1.00 | 11 |
| **Moyenne** | **1.00** | **1.00** | **1.00** | **30** |

**Interprétation des métriques** :
- **Precision** : Proportion de prédictions correctes parmi toutes les prédictions positives pour une classe
- **Recall** : Proportion d'instances correctement identifiées parmi toutes les instances réelles d'une classe
- **F1-Score** : Moyenne harmonique entre precision et recall

#### Matrice de confusion

```
                Prédictions
              Setosa  Versicolor  Virginica
    Setosa      10        0          0
Versicolor       0        9          0
 Virginica       0        0         11
```

**Analyse** : La matrice de confusion montre une classification parfaite avec aucune erreur de classification (tous les éléments sont sur la diagonale).

---

## 7. Conclusions

### Résultats obtenus

Le modèle Random Forest a démontré une **performance exceptionnelle** avec :
- Une précision de 100% sur l'ensemble de test
- Aucune erreur de classification
- Des scores parfaits pour toutes les espèces d'Iris

### Points forts du projet

1. **Qualité des données** : Dataset propre sans valeurs manquantes ni doublons
2. **Choix de l'algorithme** : Random Forest adapté pour ce type de classification multi-classes
3. **Performance optimale** : Classification parfaite sur l'ensemble de test

### Recommandations

1. **Validation croisée** : Bien que les résultats soient excellents, il serait recommandé d'effectuer une validation croisée (k-fold cross-validation) pour confirmer la robustesse du modèle
2. **Optimisation des hyperparamètres** : Explorer l'ajustement des paramètres du Random Forest (nombre d'arbres, profondeur maximale, etc.) via GridSearchCV
3. **Analyse de l'importance des variables** : Étudier quelles caractéristiques morphologiques contribuent le plus à la classification
4. **Test sur de nouvelles données** : Valider le modèle sur des données externes non vues pour confirmer sa capacité de généralisation

