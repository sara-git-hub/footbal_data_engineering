# ⚽ Projet d'Analyse de Données Football avec PySpark

## 📋 Description du Projet
Ce projet utilise **PySpark** pour une analyse approfondie des données de matches de football allemand (**Bundesliga**) sur la période **2000-2015**. L'analyse comprend le traitement de données distribué, l'agrégation de statistiques d'équipe, le calcul de classements complexes par saison et l'identification automatisée des champions.

---

## 🎯 Objectifs Clés
* **Nettoyage & Transformation :** Préparer les données brutes de matches pour l'analyse.
* **Calcul de Statistiques :** Dériver des métriques d'équipe (victoires, défaites, buts marqués/encaissés).
* **Classement Dynamique :** Déterminer le classement des équipes par saison en utilisant les **Window Functions** de PySpark.
* **Identification des Champions :** Extraire les champions de chaque saison avec leurs statistiques détaillées.
* **Visualisation :** Représenter les performances clés des équipes championnes.

---

## 🛠️ Technologies Utilisées
| Technologie | Rôle |
| :--- | :--- |
| **PySpark 3.5.1** | Traitement de données distribué et *Feature Engineering*. |
| **Python** | Langage de programmation. |
| **Pandas / Matplotlib** | Analyse de données pour la visualisation (graphiques). |
| **Jupyter/Colab** | Environnement de développement. |

---

## 📊 Structure des Données

### Données Source
Fichier CSV de matches avec les colonnes clés :
`Season`, `HomeTeam`, `AwayTeam`, `FTHG` (Buts Domicile), `FTAG` (Buts Extérieur), `FTR` (Résultat Final).

### Données Transformées
Dataset agrégé par équipe et par saison, incluant :
`GoalsScored`, `GoalsAgainst`, `GoalDifferentials`, `WinPercentage`, `TeamPosition` (Classement final).

---

## 🔄 Processus de Traitement PySpark
1.  **Chargement & Filtrage :** Lecture du CSV et isolation des données de Bundesliga (Div 1, 2000-2015).
2.  **Feature Engineering :** Création d'indicatrices de victoire/défaite/nul par match.
3.  **Agrégation :** Calcul séparé et fusion des statistiques Domicile/Extérieur pour obtenir les statistiques totales d'équipe.
4.  **Classement :** Utilisation des **Window Functions** pour classer les équipes par saison (Critères : Pourcentage de Victoires puis Différentiel de Buts).
5.  **Export :** Sauvegarde des résultats au format **Parquet partitionné** par saison.

---

## 📈 Métriques Clés Calculées
Pour chaque équipe et saison :

* **Statistiques de base :** Victoires, Défaites, Nuls.
* **Performance :** Buts marqués, Buts encaissés, **Différentiel de buts**.
* **Efficacité :** **Pourcentage de victoires**.
* **Résultat :** **Position finale** dans la ligue (`TeamPosition`).

---

## 🚀 Utilisation et Exemple
Pour interroger les données traitées directement avec PySpark :

```python
from pyspark.sql import SparkSession
from pyspark.sql import functions as F

# Supposons que 'spark' est initialisé
# df_ranked = spark.read.parquet("football_stats_partitioned")

# Charger les données des champions
df_champions = spark.read.parquet("football_top_teams")

# Afficher le classement d'une saison spécifique (exemple 2010)
# Assurez-vous d'avoir le chemin correct vers le fichier parquet partitionné
# df_ranked.filter(F.col("Season") == 2010).orderBy("TeamPosition").show(truncate=False)

print("--- Aperçu des Champions ---")
df_champions.show(5)
