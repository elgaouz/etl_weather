Projet Airflow : Pipeline ETL pour les Données Météorologiques
===============================================================

Ce projet utilise Apache Airflow pour extraire des données météorologiques de l'API Open-Meteo, les transformer, puis les charger dans une base de données PostgreSQL. Le pipeline est conçu pour s'exécuter quotidiennement et récupérer les données météorologiques pour Rabat, au Maroc.

Structure du Pipeline ETL
===========================
Ce DAG comprend trois tâches principales :

1. Extraction : Utilisation de l'API Open-Meteo pour obtenir les données météorologiques actuelles.
2. Transformation : Transformation des données extraites en un format structuré.
3. Chargement : Insertion des données transformées dans une table PostgreSQL.

Fichiers et Code
==================
Le code est organisé en un DAG Airflow unique (weather_etl_pipeline) et contient les éléments suivants :

  . Paramètres de connexion :

      .POSTGRES_CONN_ID : Identifiant de connexion Airflow pour PostgreSQL.
      .API_CONN_ID : Identifiant de connexion Airflow pour l'API Open-Meteo.
  .Détails de la localisation :

      .Coordonnées pour Rabat : LATITUDE = '34.020882' et LONGITUDE = '-6.841650'.

Code du Pipeline ETL
=====================
Le DAG weather_etl_pipeline est programmé pour s'exécuter quotidiennement avec les étapes suivantes :

1. extract_weather_data() :
  - Utilise un hook HTTP pour interagir avec l'API Open-Meteo.
  - Récupère les données de l'API pour les coordonnées spécifiées.
2. transform_weather_data(weather_data) :
  - Transforme les données JSON reçues de l'API en un dictionnaire structuré.
  - Les champs incluent latitude, longitude, temperature, windspeed, winddirection, et weathercode.
3. load_weather_data(transformed_data) :
  - Se connecte à la base de données PostgreSQL via un hook.
  - Crée une table weather_data si elle n'existe pas encore.
  - Insère les données transformées dans la table.

Conclusion
==========
Ce projet a été développé pour montrer l'intégration d'Airflow avec des sources de données API et une base de données relationnelle pour la construction de pipelines ETL efficaces.
