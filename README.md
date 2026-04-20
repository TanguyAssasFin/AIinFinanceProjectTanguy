# Modélisation du Risque de Crédit – Défaut des Clients de Carte de Crédit

---

## 1. Informations sur le projet

- **Titre du projet :** Prédiction du risque de défaut de crédit avec le Machine Learning  

- **Membre du groupe :**  
  - Tanguy CONVERSET  

- **Cours :** AI In Finance  
- **Enseignants :** Nicolas De Roux & Mohamed EL FAKIR  
- **Date de rendu :** 21 avril 2026  

---

## 2. Description du projet

Ce projet porte sur la **modélisation du risque de crédit**, avec pour objectif de prédire si un client de carte de crédit va faire défaut sur son paiement.

Les institutions financières utilisent ce type de modèle pour évaluer le risque client avant d’accorder un crédit. Une mauvaise estimation peut entraîner des pertes financières importantes, tandis qu’une prédiction fiable permet d’améliorer la prise de décision et la rentabilité.

Ce projet est particulièrement pertinent pour :
- Les banques et institutions financières  
- Les systèmes de scoring de crédit  
- Les entreprises fintech  

---

## 3. Objectif du projet

L’objectif est de **prédire si un client fera défaut le mois suivant**, à partir de données financières et comportementales.

Un modèle performant doit :
- Identifier efficacement les clients à risque  
- Aider à la prise de décision en matière de crédit  
- Fournir un score de risque fiable  

---

## 4. Définition de la tâche

- **Type de tâche :** Classification binaire  

- **Variables d’entrée :**  
  Variables financières, démographiques et comportementales telles que :
  - Limite de crédit  
  - Historique de paiement  
  - Montants facturés  
  - Montants remboursés  
  - Variables créées (utilisation du crédit, ratio de paiement, etc.)  

- **Variable cible :**  
  `default.payment.next.month`  

- **Métriques d’évaluation :**  
  - ROC-AUC  
  - F1-score  
  - Accuracy  

---

## 5. Description du dataset

### Vue d’ensemble

- **Nombre d’observations :** 30 000  
- **Nombre de variables :** 27  
- **Variable cible :** default.payment.next.month  
- **Source :** UCI Credit Card Default Dataset  

---

### Description des variables

| Variable | Description | Type |
|----------|------------|------|
| LIMIT_BAL | Limite de crédit | Numérique |
| SEX | Genre | Catégorielle |
| EDUCATION | Niveau d’éducation (nettoyé) | Catégorielle |
| MARRIAGE | Statut marital (nettoyé) | Catégorielle |
| AGE | Âge | Numérique |
| PAY_0 à PAY_6 | Historique des retards de paiement | Ordinale |
| BILL_AMT1 à BILL_AMT6 | Montants des factures | Numérique |
| PAY_AMT1 à PAY_AMT6 | Montants remboursés | Numérique |
| utilisation_credit_moy | Utilisation moyenne du crédit | Numérique |
| utilisation_credit_max | Utilisation maximale du crédit | Numérique |
| ratio_paiement | Ratio de paiement | Numérique |
| age_group | Groupe d’âge | Catégorielle |

---

### Variable cible

- **Nom :** `default.payment.next.month`  
- **Signification :** Indique si un client fera défaut le mois suivant  
- **Valeurs :**  
  - 0 → Pas de défaut  
  - 1 → Défaut  

---

### Types de données

- Variables **numériques** (montants, âge)  
- Variables **catégorielles** (genre, éducation, statut marital)  
- Variables **ordinales** (historique de paiement)  
- Variables **créées** (feature engineering)  

---

### Distribution des données

- Dataset **déséquilibré** (moins de défauts que de non-défauts)  
- Variables financières **asymétriques (skewed)**  
- Présence de valeurs extrêmes  

---

### Qualité des données

- Suppression de la colonne **ID**  
- Nettoyage des variables **EDUCATION** et **MARRIAGE**  
- Pas de valeurs manquantes significatives  
- Déséquilibre des classes  

---

## 6. Prétraitement des données

- Suppression de la colonne **ID** (non pertinente)  
- Nettoyage des variables catégorielles  
- Création de nouvelles variables :
  - `utilisation_credit_moy`
  - `utilisation_credit_max`
  - `ratio_paiement`
  - `age_group`
- Aucun scaling ni encodage appliqué (modèles d’arbres utilisés)  

---

## 7. Approche de modélisation

### Modèles utilisés

- Régression Logistique  
- Random Forest  
- XGBoost  
- MLP (réseau de neurones)  

---

### Stratégie de modélisation

- Séparation train/test  
- Régression logistique utilisée comme baseline  
- Validation croisée sur Random Forest  

Scores de validation croisée : [0.8639, 0.8625, 0.8654, 0.8854, 0.8846]


- Analyse de l’overfitting :
  - AUC train : 0.9218  
  - AUC test : 0.8786  

- Calibration des probabilités appliquée  

---

### Métriques d’évaluation

- **ROC-AUC** → adaptée aux datasets déséquilibrés  
- **F1-score** → équilibre précision / rappel  
- **Accuracy** → performance globale  

---

### Performance des modèles

#### Régression Logistique
- AUC : 0.7283  
- F1 : 0.6656  

#### Random Forest
- AUC : 0.8786  
- F1 : 0.7904  

#### XGBoost
- AUC : 0.8445  
- F1 : 0.7485  

#### MLP
- AUC : 0.8458  
- F1 : 0.7804  

---

### Meilleur modèle

👉 **Random Forest** est le modèle le plus performant.

---

### Calibration

- AUC après calibration : **0.9758**

---

## 8. Interprétabilité du modèle

### Analyse SHAP

- **PAY_0** est la variable la plus importante  
- L’historique de paiement est le facteur clé  
- Une utilisation élevée du crédit augmente le risque  
- De faibles remboursements augmentent la probabilité de défaut  

---

### Importance des variables (Top 10)

| Variable | Importance |
|----------|----------|
| PAY_0 | 0.187 |
| PAY_2 | 0.084 |
| utilisation_credit_max | 0.049 |
| PAY_3 | 0.049 |
| utilisation_credit_moy | 0.048 |
| PAY_4 | 0.044 |
| PAY_AMT1 | 0.042 |
| PAY_5 | 0.038 |
| PAY_AMT2 | 0.037 |
| BILL_AMT1 | 0.037 |

---

### Insight clé

> Le comportement de paiement passé est le meilleur prédicteur du défaut futur.

---

## 9. Installation

Installer les dépendances :

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost shap kagglehub
