# Détection de fraude financière — Transactions bancaires

Modèle de détection automatique de fraudes par carte de crédit 
sur 284 807 transactions réelles, avec comparaison de 5 approches 
de Machine Learning et optimisation du seuil de décision.

---

##  Objectif

Construire un modèle capable de détecter automatiquement les 
transactions frauduleuses parmi des centaines de milliers d'opérations 
bancaires, en minimisant les fraudes manquées (Faux Négatifs).

---

##  Données

- **Source** : Credit Card Fraud Detection (Kaggle — Machine Learning Group, ULB)
- **Période** : Transactions européennes de septembre 2013
- **Taille** : 284 807 transactions — 31 colonnes
- **Déséquilibre** : 492 fraudes (0.17%) sur 284 807 transactions

---

##  Outils utilisés

- Python, Pandas, NumPy
- Matplotlib, Seaborn (visualisation)
- Scikit-learn, XGBoost (Machine Learning)
- imbalanced-learn (SMOTE)
- Google Colab

---

##  Approche technique

**Problème identifié :** Dataset fortement déséquilibré — un modèle 
naïf qui prédit "normal" pour tout aurait 99.83% de précision 
sans détecter aucune fraude.

**5 approches comparées :**
1. Random Forest avec `class_weight='balanced'` (seuil 0.5)
2. Random Forest avec seuil de décision ajusté à 0.3
3. Random Forest entraîné sur données rééquilibrées par SMOTE
4. XGBoost (paramètres par défaut)
5. XGBoost optimisé via GridSearchCV (36 combinaisons testées)

---

##  Résultats — Comparaison des 5 approches

| Approche | Precision | Recall | Fraudes manquées | Fausses alarmes |
|---|---|---|---|---|
| Random Forest, seuil 0.5 | 96% | 76% | 24 | 3 |
| **Random Forest, seuil 0.3** | 94% | **82%** | **18** | 5 |
| Random Forest + SMOTE | 81% | 81% | 19 | 18 |
| XGBoost (brut) | 87% | 80% | 20 | 12 |
| XGBoost optimisé (GridSearchCV) | 93% | 80% | 20 | 6 |

 **Modèle retenu : Random Forest + class_weight='balanced' + seuil 0.3**

Justification : dans la détection de fraude, une fraude manquée coûte 
de l'argent réel et irréversible à la banque et au client, alors qu'une 
fausse alarme ne coûte qu'un appel de vérification. Le Recall — qui 
mesure les fraudes manquées — doit donc primer sur la Precision. 
Ce modèle minimise le plus les Faux Négatifs parmi les 5 approches testées.

---

##  Variable la plus importante

**V14** est la variable la plus déterminante (importance ≈ 0.20).
Les transactions frauduleuses ont des valeurs de V14 très différentes 
des transactions normales.

---

##  Concepts clés appliqués

- **Indice de Gini** : mesure de l'impureté utilisée par les arbres 
  de décision pour choisir leurs coupures
- **Bagging** : chaque arbre du Random Forest s'entraîne sur un 
  échantillon aléatoire différent, réduisant le surapprentissage
- **Boosting (XGBoost)** : chaque arbre corrige les erreurs du 
  précédent, de façon séquentielle
- **SMOTE** : génère des fraudes synthétiques pour équilibrer les 
  classes sans dupliquer les données existantes
- **GridSearchCV** : recherche automatique des meilleurs 
  hyperparamètres via validation croisée

---

##  Limites et améliorations possibles

- Variables anonymisées par PCA — interprétabilité limitée
- Recall de 82% : 18 fraudes sur 98 encore manquées
- Améliorations possibles :
  - Élargir la grille GridSearchCV (plus de combinaisons testées)
  - Combiner XGBoost avec un seuil ajusté (comme fait pour Random Forest)
  - Réseaux de neurones (autoencoders) pour la détection d'anomalies

---

##  Auteur

**Ezekiel Hoffer Koffi** — Analyste de données, Lomé, Togo  
GitHub : [github.com/ezekiel-oos](https://github.com/ezekiel-oos)
