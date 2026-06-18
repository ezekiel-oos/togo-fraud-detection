# Détection de fraude financière — Transactions bancaires

Modèle de détection automatique de fraudes par carte de crédit 
sur 284 807 transactions réelles, avec Random Forest et optimisation 
du seuil de décision.

---

##  Objectif

Construire un modèle capable de détecter automatiquement les 
transactions frauduleuses parmi des centaines de milliers d'opérations 
bancaires, en minimisant les fraudes manquées (Faux Négatifs).

---

## Données

- **Source** : Credit Card Fraud Detection (Kaggle — Machine Learning Group, ULB)
- **Période** : Transactions européennes de septembre 2013
- **Taille** : 284 807 transactions — 31 colonnes
- **Déséquilibre** : 492 fraudes (0.17%) sur 284 807 transactions

---

##  Outils utilisés

- Python, Pandas, NumPy
- Matplotlib, Seaborn (visualisation)
- Scikit-learn (Machine Learning)
- Google Colab

---

## Approche technique

**Problème identifié :** Dataset fortement déséquilibré — un modèle 
naïf qui prédit "normal" pour tout aurait 99.83% de précision 
sans détecter aucune fraude.

**Solutions appliquées :**
- Normalisation de `Amount` et `Time` avec `StandardScaler`
- `class_weight='balanced'` pour pénaliser les fraudes manquées
- Ajustement du seuil de décision de 0.5 à 0.3 pour améliorer le Recall

---

## Résultats

| Métrique | Seuil 0.5 (défaut) | Seuil 0.3 (optimisé) |
|---|---|---|
| Precision | 96% | 94% |
| Recall | 76% | **82%** |
| Fraudes manquées | 24 | **18** |
| Fausses alarmes | 3 | 5 |

 L'ajustement du seuil détecte **6 fraudes supplémentaires** 
au prix de seulement 2 fausses alarmes en plus.

---

##  Variable la plus importante

**V14** est la variable la plus déterminante (importance ≈ 0.20).
Les transactions frauduleuses ont des valeurs de V14 très différentes 
des transactions normales.

---

##  Limites et améliorations possibles

- Variables anonymisées par PCA — interprétabilité limitée
- Recall de 82% : 18 fraudes sur 98 encore manquées
- Améliorations possibles :
  - SMOTE (rééchantillonnage de la classe minoritaire)
  - XGBoost ou LightGBM
  - Optimisation par GridSearchCV

---

## 👤 Auteur

**Ezekiel Hoffer Koffi** — Analyste de données, Lomé, Togo  
GitHub : [github.com/ezekiel-oos](https://github.com/ezekiel-oos)
