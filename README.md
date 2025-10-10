Projet d'Analyse de Données Football avec PySpark
📋 Description du Projet
Ce projet utilise PySpark pour analyser des données de matches de football allemand (Bundesliga) sur la période 2000-2015. L'analyse comprend le traitement de données, l'agrégation de statistiques d'équipe, le calcul de classements et l'identification des champions par saison.

🎯 Objectifs
Nettoyer et transformer les données brutes de matches de football

Calculer des statistiques d'équipe (victoires, défaites, buts marqués/encaissés)

Déterminer le classement des équipes par saison

Identifier les champions de chaque saison

Visualiser les performances des équipes championnes

🛠️ Technologies Utilisées
PySpark 3.5.1 - Traitement distribué des données

Python - Langage de programmation

Pandas - Analyse de données pour visualisation

Matplotlib - Création de graphiques

Jupyter/Colab - Environnement de développement

📊 Structure des Données
Données Source
Le fichier CSV original contient les colonnes suivantes :

Match_ID, Div (Division), Season, Date

HomeTeam, AwayTeam (Équipes à domicile et extérieur)

FTHG, FTAG (Buts marqués à domicile et à l'extérieur)

FTR (Résultat final: H=Victoire domicile, A=Victoire extérieur, D=Match nul)

Données Transformées
Après traitement, le dataset inclut :

Statistiques par équipe et par saison

Pourcentages de victoires/défaites/nuls

Différentiel de buts

Classement final

Métriques de performance

🔄 Processus de Traitement
1. Chargement et Nettoyage
Lecture du fichier CSV

Renommage des colonnes pour plus de clarté

Filtrage sur la Division 1 (2000-2015)

2. Feature Engineering
Création de colonnes supplémentaires :

HomeTeamWin / AwayTeamWin / GameTie (indicatrices binaires)

Agrégation des statistiques par équipe et saison

3. Agrégation et Jointure
Calcul des statistiques à domicile et à l'extérieur

Fusion des DataFrames home/away

Création de métriques synthétiques :

GoalsScored, GoalsAgainst

WinPercentage, GoalDifferentials

GoalsPerGame, GoalsAgainstPerGame

4. Classement
Utilisation des Window Functions pour :

Classer les équipes par saison

Priorité : Pourcentage de victoires → Différentiel de buts

5. Export et Visualisation
Sauvegarde en format Parquet partitionné

Génération de graphiques pour les équipes championnes

📈 Métriques Calculées
Pour chaque équipe et saison :

Statistiques de base : Victoires, Défaites, Nuls

Performance offensive : Buts marqués, Buts par match

Performance défensive : Buts encaissés, Buts contre par match

Efficacité : Pourcentage de victoires, Différentiel de buts

Classement : Position finale dans la ligue

🏆 Résultats Principaux
Le projet identifie automatiquement les champions de Bundesliga pour chaque saison entre 2000 et 2015, avec leurs statistiques détaillées.

📁 Structure des Fichiers de Sortie
football_stats_partitioned/ - Dataset complet partitionné par saison

football_top_teams/ - Statistiques des équipes championnes

🚀 Utilisation
python
# Charger les données traitées
df_ranked = spark.read.parquet("football_stats_partitioned")
df_champions = spark.read.parquet("football_top_teams")

# Afficher le classement d'une saison spécifique
df_ranked.filter(F.col("Season") == 2010).orderBy("TeamPosition").show()
📊 Visualisations Disponibles
Pourcentage de victoires des champions - Évolution de la dominance

Buts marqués par les champions - Performance offensive

Différentiel de buts - Mesure de la supériorité globale

🔍 Insights Potentiels
Ce dataset permet d'analyser :

L'évolution de la compétitivité de la ligue

Les caractéristiques des équipes championnes

Les tendances offensives/défensives au fil du temps

La performance relative des équipes à domicile vs extérieur

📝 Notes
Les données couvrent 16 saisons de Bundesliga

Toutes les équipes sont analysées sur la même base (34 matches/saison)

Le classement utilise des critères standard (points → différentiel de buts)
