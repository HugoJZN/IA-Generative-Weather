Voici une reformulation fluide et professionnelle du résumé, en conservant le fond tout en variant le style et le vocabulaire :


## Synthèse du projet – Prédiction des précipitations (RainTomorrow)

### Objectif du projet

L’objectif est de **déterminer la probabilité de pluie le jour suivant** (`RainTomorrow`) à partir de données météorologiques historiques. Plusieurs algorithmes de **machine learning** sont comparés, avec une attention particulière portée à l’effet de la **réduction de dimension par ACP (PCA)** sur les performances des modèles.


### Description des données

* **Jeu de données** : `Data_Weather.csv`
* **Volume** : 145 460 observations, 22 variables explicatives
* **Variable cible** : `RainTomorrow` (Oui / Non)
* **Déséquilibre des classes** :

  * No : ~78 %
  * Yes : ~22 %


### Analyse exploratoire des données (EDA)

* Aucune valeur manquante détectée après vérification
* Étude des distributions statistiques et des corrélations entre variables
* Visualisation claire du déséquilibre de la variable cible


### Prétraitement

* Suppression des variables peu informatives (`Date`, `Location`)
* Encodage binaire de la cible (Yes = 1, No = 0)
* Division des données en **ensemble d’entraînement et de test (80 % / 20 %)** avec stratification
* Mise en place d’un pipeline appliqué uniquement sur le jeu d’entraînement :

  * Imputation des valeurs manquantes
  * Détection et traitement des valeurs aberrantes via la méthode IQR
  * Encodage One-Hot des variables catégorielles
  * Normalisation des variables numériques
  * Élimination des variables fortement corrélées
  * Rééquilibrage des classes à l’aide de **SMOTE**


### Réduction de dimension par PCA

* Nombre de variables avant PCA : **60**
* Conservation de **75 % de la variance expliquée**
* Nombre de composantes principales retenues : **31**
* Diminution de la dimensionnalité : **–48 %**


### Modèles évalués

1. **Régression logistique**
2. **KNN sans réduction de dimension**
3. **KNN avec PCA**

Les hyperparamètres du modèle KNN ont été optimisés à l’aide de **GridSearchCV**.


### Performances (ensemble de test)

La **régression logistique** présente les meilleures performances globales, en particulier sur les métriques **ROC-AUC** et **F1-score**. Le **KNN**, quant à lui, montre une forte sensibilité à la dimensionnalité des données, avec une baisse de performance après application du PCA.


### Interprétation des résultats

L’étude des coefficients du modèle de régression logistique met en évidence que :

* **Humidity3pm** est la variable la plus influente
* La vitesse et l’orientation du vent constituent également des facteurs clés dans la prédiction des épisodes pluvieux


### Analyses et visualisations détaillées

L’ensemble des **graphiques, comparaisons approfondies, matrices de confusion, courbes ROC, validations croisées et métriques complètes** pour les modèles **KNN** et **régression logistique** est disponible dans le notebook GitHub suivant :


### Conclusion

* La **régression logistique** offre le meilleur équilibre entre performance prédictive et interprétabilité
* L’**ACP (PCA)** permet une réduction efficace de la dimension, mais au prix d’une légère dégradation des performances du KNN
* Le rééquilibrage des classes avec **SMOTE** améliore significativement la détection des jours de pluie

**Modèle final recommandé : Régression logistique sans PCA**
