<div align="center">

# Google Trends Analytics
### Analyse des tendances de recherche · Data Visualization · Streamlit

**Un pipeline de données et une application interactive pour comparer cinq sujets à travers le temps, les pays et les continents.**

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white) ![Google Trends](https://img.shields.io/badge/Google-Trends-4285F4?logo=google&logoColor=white)

</div>

---

## Le projet en un coup d'œil

| Mots-clés analysés | Échelle | Séries temporelles | Analyse géographique |
|:---:|:---:|:---:|:---:|
| **5** | **Mondiale** | **3 ans** | **Pays et continents** |

**Sujets étudiés :** Intelligence artificielle · Crypto · Netflix · Tesla · ChatGPT

> **À savoir :** Google Trends fournit des indices relatifs de popularité (0 à 100), et non le nombre réel de recherches. Les comparaisons doivent être interprétées dans ce cadre.

## Aperçu des visualisations

### Évolution des recherches

![Évolution temporelle des tendances](outputs/figures_premium_dark/01_search_momentum_dark.png)

### Carte mondiale des mots-clés dominants

![Carte mondiale des tendances](outputs/figures_premium_dark/03_world_leaders_dark.png)

| Saisonnalité des recherches | Popularité et domination locale |
|---|---|
| ![Heatmap mensuelle](outputs/figures_premium_dark/02_monthly_heatmap_dark.png) | ![Popularité et domination](outputs/figures_premium_dark/04_popularity_vs_dominance_dark.png) |

### Comparaison par continent

![Comparaison des tendances par continent](outputs/figures_premium_dark/05_continental_leaders_dark.png)

## Parcours des données

`Google Trends (pytrends) → Nettoyage et normalisation → Enrichissement géographique → Indicateurs → Visualisations → Application Streamlit`

### Accès rapide

[**Application Streamlit**](app/streamlit_app.py) · [**Scripts de traitement**](scripts/) · [**Graphiques**](outputs/figures_premium_dark/) · [**Dépendances**](requirements.txt)

---

<details>
<summary><strong>Afficher la documentation complète : méthodologie, données et exécution</strong></summary>

##  Objectif du projet

Ce projet vise à analyser et comparer l’intérêt relatif pour 5 mots-clés à l’échelle mondiale, en combinant :

- des données issues de Google Trends
- un enrichissement par métadonnées pays (type Kaggle)
- des visualisations interactives via Streamlit

L’objectif est de construire une pipeline data complète allant de la collecte à l’interprétation.

---

##  Problématique

Comment comparer l’intérêt pour différents mots-clés :

- dans le temps  
- selon les pays  
- et selon les zones géographiques  

tout en tenant compte du fait que Google Trends fournit des données relatives (0–100) et non absolues ?

---

##  Architecture du projet

##  Structure du projet

```
projet_trends/
│
├── data/
│   ├── raw/                  # données brutes Google Trends
│   ├── processed/            # datasets nettoyés et enrichis
│   └── kaggle/               # métadonnées pays
│
├── scripts/
│   ├── collect_trends.py
│   ├── clean_merge.py
│   ├── country_insights.py
│   └── graphs_final.py
│
├── app/
│   └── streamlit_app.py
│
├── outputs/
│   └── figures/
│
├── requirements.txt
└── README.md
```
---

##  Pipeline de traitement

### 1. Collecte des données

Script : collect_trends.py

- récupération via pytrends
- 5 mots-clés :
  - intelligence artificielle
  - crypto
  - Netflix
  - Tesla
  - ChatGPT

Deux datasets :

- trends_time.csv
  - évolution temporelle (3 ans)

- trends_country.csv
  - distribution géographique (1 an)

---

### 2. Nettoyage et structuration

Script : clean_merge.py

Transformations :

- conversion en format long
- normalisation des noms de pays
- mapping FR → EN
- gestion des valeurs manquantes

---

### 3. Enrichissement des données

Ajout de métadonnées pays :

- code ISO3
- continent
- région

 Permet :

- cartes interactives
- agrégations géographiques
- analyses comparatives

---

### 4. Calcul des indicateurs

Script : country_insights.py

Variables créées :

- mot_cle_dominant
- score_max
- score_2eme
- ecart_top2

 Permet d’identifier :

- le mot-clé dominant par pays
- l’intensité de domination
- la concurrence entre mots-clés

---

### 5. Visualisation

#### Application Streamlit

L’application permet :

- sélection de mots-clés
- filtrage par continent
- visualisation interactive :
  - courbes temporelles
  - top pays
  - carte mondiale
  - indicateurs clés

---

##  Graphes utilisés pour les slides

1. Search Momentum
→ montre l’évolution globale et les pics d’intérêt dans le temps

2. Monthly Heatmap
→ met en évidence les périodes fortes et les tendances saisonnières

3. World Leaders
→ visualise le mot-clé dominant dans chaque pays

4. Popularity vs Dominance
→ compare la popularité d’un mot-clé et sa domination locale

5. Continental Leaders
→ identifie le mot-clé le plus fort en moyenne par continent


##  Limites du projet

- Google Trends fournit un score relatif (0–100)  
- pas de volume absolu de recherche  
- dépendance à une API non officielle (pytrends)  
- qualité variable des données pays  

---

##  Lancer le projet

### 1. Installer les dépendances

bash pip install -r requirements.txt 

### 2. Collecter les données

bash python scripts/collect_trends.py 

### 3. Nettoyer et enrichir

bash python scripts/clean_merge.py 

### 4. Générer les insights

bash python scripts/country_insights.py 

### 5. Lancer l’application

bash python -m streamlit run app/streamlit_app.py 

---

##  Résultats principaux

- certains mots-clés dominent largement selon les zones géographiques  
- la popularité varie fortement selon les pays  
- certains mots-clés présentent une distribution homogène  
- d’autres sont très localisés  

---

##  Apports du projet

Ce projet illustre :

- la construction d’une pipeline data complète  
- l’intégration de sources multiples  
- la transformation de données brutes en indicateurs  
- la visualisation et l’interprétation de données  

---

##  Améliorations possibles

- ajout d’autres mots-clés  
- intégration de nouvelles sources de données  
- analyse de tendances plus avancée  
- prévision (time series)  
- déploiement web de l’application  

---

##  Auteur

Projet réalisé dans le cadre d’un projet académique en data avec comme participant Can Pekgoz et Vanilla Nirinah Rafidison

</details>
