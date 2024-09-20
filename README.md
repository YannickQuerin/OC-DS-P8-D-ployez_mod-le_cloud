# Déploiement d'un Modèle dans le Cloud

Ce projet vise à déployer un modèle de classification d'images dans un environnement Big Data sur le cloud AWS, en utilisant Spark pour le traitement distribué et MobileNetV2 pour la reconnaissance d'images.

## Table des Matières

1. [Problématique et jeu de données](#problématique-et-jeu-de-données)
2. [Processus de création de l’environnement Big Data](#processus-de-création-de-lenvironnement-big-data)
3. [Chaîne de traitement d’images dans le cloud](#chaîne-de-traitement-dimages-dans-le-cloud)
4. [Démonstration d'exécution du script Spark dans le Cloud](#démonstration-dexécution-du-script-spark-dans-le-cloud)
5. [Conclusion](#conclusion)

---

## Problématique et Jeu de Données

### Contexte de l'entreprise
**Fruits**, une start-up de l'AgriTech, propose une application mobile de reconnaissance de fruits par photographie. Le projet est divisé en deux phases :
- Phase 1 : Classification d’images avec un volume accru de données.
- Phase 2 : Développement de robots cueilleurs intelligents.

### Mission
Mettre en place une architecture Big Data pour la classification d’images à des fins d’application mobile.

### Objectifs
- Promouvoir l'application mobile via une architecture évolutive.
- Réaliser un traitement distribué pour répondre à un volume croissant d’images.

### Jeu de Données
- **Base de données Fruits 360** de Kaggle.
- **90 380 images** réparties en **131 classes** (ex. : pomme, banane, fraise, etc.).
- Taille des images : **100x100 pixels** sur fond blanc.
- Images organisées par classe avec différentes perspectives pour chaque fruit.

---

## Processus de Création de l’Environnement Big Data

### Outils et Infrastructure

- **Apache Spark** : Framework de calcul distribué.
- **Algorithme MapReduce** : Traitement parallèle pour optimiser les calculs.
- **AWS** : Plateforme cloud utilisée pour l’hébergement et la gestion des données.
- **PuTTY** : Outil pour les connexions SSH.
- **JupyterHub** : Utilisé pour exécuter les scripts PySpark.

### Configuration de l’Environnement
1. **Gestion des accès** avec IAM (Identity and Access Management).
2. **Stockage des données** sur Amazon S3.
3. **Création d'un cluster EMR** (Elastic MapReduce) pour le traitement distribué.
4. **Tunnel SSH** pour accéder à l’EMR via PuTTY et FoxyProxy.

---

## Chaîne de Traitement d’Images dans le Cloud

### Préprocessing des Images
1. Chargement des images depuis **Amazon S3** dans un DataFrame Spark.
2. Utilisation de **PIL** pour redimensionner les images à **224x224 pixels**.
3. Prétraitement avec la fonction `preprocess_input` de **TensorFlow** pour adapter les images au modèle.

### Modèle MobileNetV2 et Extraction des Features
- Modèle de réseau de neurones **MobileNetV2**, pré-entraîné sur **ImageNet**.
- **Transfer Learning** : Utilisation de la couche avant-dernière pour extraire les features.
- Stockage des features extraits dans des fichiers **Parquet** sur Amazon S3.

### Réduction de Dimension
Application de la **PCA** (Analyse en Composantes Principales) pour réduire la dimensionnalité des features extraits.

---

## Démonstration d'Exécution du Script Spark dans le Cloud

Exécution du script PySpark sur un **notebook Jupyter** hébergé sur le cluster EMR. Les étapes principales incluent :
- Démarrage d'une session Spark.
- Chargement et traitement des images.
- Extraction des features avec **MobileNetV2**.
- Écriture des résultats dans Amazon S3.

---

## Conclusion

Le projet met en place une architecture Big Data évolutive et performante, répondant aux besoins de la start-up **Fruits**. L’utilisation de technologies telles que **Spark**, **AWS S3**, et **MobileNetV2** permet de gérer efficacement des volumes massifs d’images et de préparer l’entreprise à un futur passage à l'échelle.

