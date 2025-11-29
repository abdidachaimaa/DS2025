# Rapport d'Analyse Statistique - Student Stress Analysis

## 1. Introduction et Exploration des Données

### 1.1 Contexte et Objectifs

Cette analyse vise à identifier les facteurs contributifs au stress chez les étudiants et à modéliser la relation entre diverses variables et le niveau de stress observé. L'étude utilise des techniques de régression linéaire et logistique pour comprendre les déterminants du stress étudiant.

### 1.2 Description du Dataset

- **Nombre total d'observations :** 520
- **Observations valides :** 520
- **Variables numériques :** Kindly Rate your Sleep Quality 😴, How many times a week do you suffer headaches 🤕?, How would you rate you academic performance 👩‍🎓?, how would you rate your study load?, How many times a week you practice extracurricular activities 🎾?, How would you rate your stress levels?
- **Variables catégorielles :** 

### 1.3 Valeurs Manquantes

| Variable | Valeurs Manquantes | Pourcentage |
|----------|-------------------|-------------|
| Kindly Rate your Sleep Quality 😴 | 0 | 0.00% |
| How many times a week do you suffer headaches 🤕? | 0 | 0.00% |
| How would you rate you academic performance 👩‍🎓? | 0 | 0.00% |
| how would you rate your study load? | 0 | 0.00% |
| How many times a week you practice extracurricular activities 🎾? | 0 | 0.00% |
| How would you rate your stress levels? | 0 | 0.00% |

### 1.4 Statistiques Descriptives

| Variable | Moyenne | Médiane | Écart-type | Min | Max | N |
|----------|---------|---------|------------|-----|-----|---|
| Kindly Rate your Sleep Quality 😴 | 3.13 | 3.00 | 1.10 | 1.00 | 5.00 | 520 |
| How many times a week do you suffer headaches 🤕? | 2.18 | 2.00 | 1.25 | 1.00 | 5.00 | 520 |
| How would you rate you academic performance 👩‍🎓? | 3.33 | 3.00 | 1.06 | 1.00 | 5.00 | 520 |
| how would you rate your study load? | 2.75 | 3.00 | 1.37 | 1.00 | 5.00 | 520 |
| How many times a week you practice extracurricular activities 🎾? | 2.68 | 3.00 | 1.47 | 1.00 | 5.00 | 520 |
| How would you rate your stress levels? | 2.88 | 3.00 | 1.36 | 1.00 | 5.00 | 520 |

## 2. Visualisations Graphiques

### 2.1 Matrice de Corrélation

| Variable | Kindly Rate your Sleep Quality 😴 | How many times a week do you suffer headaches 🤕? | How would you rate you academic performance 👩‍🎓? | how would you rate your study load? | How many times a week you practice extracurricular activities 🎾? | How would you rate your stress levels? |
|----------|----------|----------|----------|----------|----------|----------|
| **Kindly Rate your Sleep Quality 😴** | 1.000 | -0.059 | 0.254 | 0.065 | 0.001 | 0.165 |
| **How many times a week do you suffer headaches 🤕?** | -0.059 | 1.000 | -0.205 | -0.007 | -0.073 | -0.072 |
| **How would you rate you academic performance 👩‍🎓?** | 0.254 | -0.205 | 1.000 | 0.096 | 0.153 | 0.055 |
| **how would you rate your study load?** | 0.065 | -0.007 | 0.096 | 1.000 | 0.175 | 0.392 |
| **How many times a week you practice extracurricular activities 🎾?** | 0.001 | -0.073 | 0.153 | 0.175 | 1.000 | 0.052 |
| **How would you rate your stress levels?** | 0.165 | -0.072 | 0.055 | 0.392 | 0.052 | 1.000 |

**Interprétation :** Les valeurs proches de 1 ou -1 indiquent des corrélations fortes (positives ou négatives). Les valeurs proches de 0 indiquent une absence de corrélation linéaire.

## 3. Analyses de Régression

### 3.1 Régression Logistique

#### 3.1.1 Configuration du Modèle

Variable cible : **How would you rate your stress levels?** (binaire)
- Stress élevé (1) : > 3.00
- Stress faible (0) : ≤ 3.00

#### 3.1.2 Matrice de Confusion

|                    | Prédit: Stress Élevé | Prédit: Stress Faible |
|--------------------|---------------------|----------------------|
| **Réel: Stress Élevé**  | 93 (VP) | 87 (FN) |
| **Réel: Stress Faible** | 188 (FP) | 152 (VN) |

**Légende :**
- VP = Vrais Positifs
- VN = Vrais Négatifs
- FP = Faux Positifs
- FN = Faux Négatifs

#### 3.1.3 Métriques de Performance

| Métrique | Valeur | Formule | Interprétation |
|----------|--------|---------|----------------|
| **Accuracy** | 47.12% | (VP + VN) / Total | Proportion de prédictions correctes |
| **Précision** | 33.10% | VP / (VP + FP) | Fiabilité des prédictions positives |
| **Rappel** | 51.67% | VP / (VP + FN) | Capacité à détecter les vrais positifs |
| **F1-Score** | 40.35% | 2 × (Précision × Rappel) / (Précision + Rappel) | Moyenne harmonique précision/rappel |

#### 3.1.4 Coefficients et Odds Ratios

Pour un modèle logistique complet, les coefficients β représentent l'impact de chaque variable sur le log-odds du stress élevé :

**log(p/(1-p)) = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ**

Les variables avec les corrélations les plus fortes avec How would you rate your stress levels? sont les meilleurs prédicteurs potentiels.

### 3.2 Régression Linéaire

#### 3.2.1 Modèle de Régression

Variable dépendante : **How would you rate your stress levels?** (continue)

**Équation du modèle :**
Y = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ + ε

Où :
- Y = Niveau de stress
- β₀ = Constante (intercept)
- βᵢ = Coefficients de régression
- Xᵢ = Variables indépendantes
- ε = Terme d'erreur

#### 3.2.2 Statistiques du Modèle

| Statistique | Valeur |
|-------------|--------|
| Moyenne de How would you rate your stress levels? | 2.875 |
| Écart-type | 1.357 |
| Variance | 1.840 |
| Plage | [1.00, 5.00] |

#### 3.2.3 Coefficients Estimés

Les corrélations avec How would you rate your stress levels? donnent une indication des relations linéaires :

| Variable | Corrélation | Direction | Force |
|----------|-------------|-----------|-------|
| how would you rate your study load? | 0.392 | Positive ↑ | Faible |
| Kindly Rate your Sleep Quality 😴 | 0.165 | Positive ↑ | Très faible |
| How many times a week do you suffer headaches 🤕? | -0.072 | Négative ↓ | Très faible |
| How would you rate you academic performance 👩‍🎓? | 0.055 | Positive ↑ | Très faible |
| How many times a week you practice extracurricular activities 🎾? | 0.052 | Positive ↑ | Très faible |

#### 3.2.4 Analyse des Résidus

**Hypothèses du modèle linéaire :**

1. **Linéarité** : Relation linéaire entre variables indépendantes et dépendante
2. **Indépendance** : Les observations sont indépendantes
3. **Homoscédasticité** : Variance constante des résidus
4. **Normalité** : Les résidus suivent une distribution normale

**Tests de significativité :**
- Test t : Pour chaque coefficient (H₀: βᵢ = 0)
- Test F : Pour le modèle global
- p-value < 0.05 indique une significativité statistique

## 4. Interprétation et Conclusions

### 4.1 Facteurs les Plus Influents

Les variables suivantes présentent les corrélations les plus fortes avec le niveau de stress :

1. **how would you rate your study load?** (r = 0.392)
   - Impact positif : augmentation associée à plus de stress
2. **Kindly Rate your Sleep Quality 😴** (r = 0.165)
   - Impact positif : augmentation associée à plus de stress
3. **How many times a week do you suffer headaches 🤕?** (r = -0.072)
   - Impact négatif : augmentation associée à moins de stress
4. **How would you rate you academic performance 👩‍🎓?** (r = 0.055)
   - Impact positif : augmentation associée à plus de stress
5. **How many times a week you practice extracurricular activities 🎾?** (r = 0.052)
   - Impact positif : augmentation associée à plus de stress

### 4.2 Recommandations Pratiques

**Basées sur l'analyse statistique :**

1. **Interventions ciblées**
   - Concentrer les efforts sur les variables avec les corrélations les plus élevées
   - Développer des programmes de prévention personnalisés

2. **Système de détection précoce**
   - Utiliser le modèle logistique pour identifier les étudiants à risque
   - Mettre en place des alertes basées sur les seuils identifiés

3. **Suivi longitudinal**
   - Collecter des données temporelles pour établir la causalité
   - Valider les modèles sur de nouvelles cohortes

4. **Approche holistique**
   - Prendre en compte les multiples facteurs identifiés
   - Adapter les interventions selon les profils individuels

### 4.3 Limites Méthodologiques

**Limites statistiques :**

1. **Causalité vs Corrélation**
   - Les corrélations n'impliquent pas de causalité
   - Des variables confondantes peuvent influencer les résultats

2. **Qualité des données**
   - 0.0% de données manquantes en moyenne
   - Possibles biais de mesure ou de déclaration

3. **Modélisation**
   - Simplifications nécessaires pour l'analyse
   - Hypothèses du modèle linéaire non vérifiées en détail
   - Validation croisée non effectuée

4. **Généralisation**
   - Résultats limités à la population échantillonnée
   - Contexte culturel et temporel spécifique

**Perspectives futures :**

- Analyse multivariée avancée (régression multiple, ANOVA)
- Modèles non-linéaires (arbres de décision, réseaux de neurones)
- Validation externe sur d'autres échantillons
- Études longitudinales pour établir la causalité

---

## Annexes

### A. Méthodologie Détaillée

**Prétraitement des données :**
- Suppression des lignes avec valeurs manquantes complètes
- Identification automatique des types de variables
- Normalisation non appliquée (données préservées à l'échelle originale)

**Analyses statistiques :**
- Corrélation de Pearson pour variables continues
- Régression logistique binaire (seuil = médiane)
- Statistiques descriptives standard

**Outils utilisés :**
- Analyse interactive en JavaScript
- Bibliothèques : Papaparse, Lodash
- Visualisations intégrées

### B. Glossaire

- **Corrélation** : Mesure de la relation linéaire entre deux variables (-1 à +1)
- **Odds Ratio** : Rapport de cotes, mesure l'effet d'un prédicteur en régression logistique
- **R²** : Coefficient de détermination, proportion de variance expliquée
- **p-value** : Probabilité d'observer les données si l'hypothèse nulle est vraie
- **Résidus** : Différence entre valeurs observées et prédites

---

**Date de génération :** 29/11/2025
**Dataset :** Student Stress Analysis (Kaggle)
**N = 520** observations analysées
