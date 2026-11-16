<div align="center">

# Google Trends Analytics

### Tendances de recherche, visualisation et Streamlit

**Un pipeline Python et une application interactive pour explorer cinq sujets dans le temps et selon les pays.**

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white) ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?logo=streamlit&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white) ![Google Trends](https://img.shields.io/badge/Google-Trends-4285F4?logo=google&logoColor=white)

</div>

## Présentation

Ce projet académique associe collecte Google Trends, préparation de données, enrichissement géographique et visualisation Streamlit.

Les cinq mots-clés étudiés sont **intelligence artificielle, crypto, Netflix, Tesla et ChatGPT**. Google Trends fournit des indices relatifs de 0 à 100, pas des volumes de recherches.

[Application et guide](app/README.md) | [Scripts Python](scripts/) | [Graphiques](outputs/figures_premium_dark/) | [Dépendances](requirements.txt)

## Périodes étudiées

| Extraction | Période configurée | Périmètre |
|---|---|---|
| Séries temporelles | Du 1er janvier 2023 au 1er janvier 2026 | Cinq mots-clés interrogés ensemble, au niveau mondial |
| Indices géographiques | Du 1er janvier 2025 au 1er janvier 2026 | Une requête distincte par mot-clé, par pays |

Ces périodes correspondent aux paramètres de `scripts/collect_trends.py`. Le dépôt conserve des extractions et des fichiers préparés ; il ne décrit pas une actualisation permanente.

## Aperçu des visualisations

### Évolution temporelle

![Évolution des indices de recherche](outputs/figures_premium_dark/01_search_momentum_dark.png)

| Matrice mensuelle | Comparaison exploratoire des indices |
|---|---|
| ![Indices par mois](outputs/figures_premium_dark/02_monthly_heatmap_dark.png) | ![Indice maximal et écart entre indices](outputs/figures_premium_dark/04_popularity_vs_dominance_dark.png) |

### Cartographie exploratoire

![Carte des indices sélectionnés par l'algorithme](outputs/figures_premium_dark/03_world_leaders_dark.png)

![Comparaison exploratoire par continent](outputs/figures_premium_dark/05_continental_leaders_dark.png)

Les figures géographiques utilisent des indices provenant de requêtes séparées. Les notions de « leader » et de « domination » décrivent le calcul exploratoire du projet, pas un classement fiable des volumes de recherche entre sujets.

## Étapes du traitement

| Étape | Fichier | Travail réalisé |
|---|---|---|
| Collecte | `scripts/collect_trends.py` | Interrogation de Google Trends avec pytrends et export CSV |
| Préparation | `scripts/clean_merge.py` | Mise au format long, harmonisation des pays et enrichissement géographique |
| Indicateurs | `scripts/country_insights.py` | Calcul des deux meilleurs indices et de leur écart par pays |
| Figures | `scripts/slides_graphs.py` | Production des cinq figures de présentation |
| Exploration | `app/streamlit_app.py` | Filtres, séries temporelles, cartes, comparaisons et résumé calculé |

## Organisation du dépôt

| Emplacement | Contenu |
|---|---|
| `data/raw/` | Extractions Google Trends |
| `data/kaggle/country_metadata.csv` | Métadonnées pays utilisées pour l'enrichissement |
| `data/processed/` | Données préparées et indicateurs |
| `scripts/` | Collecte, préparation, indicateurs et figures |
| `app/` | Application et documentation d'utilisation |
| `outputs/figures_premium_dark/` | Cinq graphiques PNG |

## Lancer l'application

Avec Git et Python disponibles :

```bash
git clone https://github.com/NacPKZ/Google-Trends-Analytics.git
cd Google-Trends-Analytics
python -m venv .venv
```

Activer `.venv` avec `.\.venv\Scripts\Activate.ps1` sous PowerShell, ou `source .venv/bin/activate` sous Linux et macOS.

```bash
python -m pip install -r requirements.txt
python -m streamlit run app/streamlit_app.py
```

Les fichiers préparés sont fournis dans le dépôt. Ils permettent d'ouvrir l'application sans relancer la collecte. Voir le [guide de l'application](app/README.md) pour les métriques et les fichiers attendus.

## Régénérer les données

Cette étape est facultative pour consulter les données versionnées. Elle interroge un service externe et remplace les sorties des scripts :

```bash
python scripts/collect_trends.py
python scripts/clean_merge.py
python scripts/country_insights.py
```

Pour générer les graphiques de présentation :

```bash
python scripts/slides_graphs.py
```

L'export PNG de Plotly nécessite un moteur d'export compatible, notamment Kaleido. Vérifier les dépendances locales si cette étape échoue. Une collecte via pytrends peut également échouer ou être limitée par Google.

## Limites

- Les indices sont relatifs et dépendent du périmètre, de la période et des mots-clés.
- Les extractions géographiques sont normalisées séparément pour chaque sujet. Leurs valeurs ne permettent pas de conclure qu'un mot-clé est davantage recherché qu'un autre dans un même pays.
- Les calculs de domination et leurs écarts sont donc exploratoires. Pour comparer les niveaux entre mots-clés, il faudrait reconstruire la collecte sur une échelle commune.
- Les périodes des séries temporelles et des données géographiques diffèrent.
- La langue des mots-clés, les métadonnées pays et le traitement des valeurs manquantes influencent les résultats.
- La collecte repose sur pytrends, une interface non officielle. Cette revue documentaire ne constitue pas une réexécution du pipeline.

## Compétences travaillées

Collecte et préparation Python, fusion de sources, données géographiques, calcul d'indicateurs, graphiques Plotly et application Streamlit. Le projet permet aussi de discuter les conditions nécessaires pour comparer des indices normalisés.

## Évolutions possibles

Revoir le protocole de collecte géographique, documenter les contrôles qualité et les métadonnées de chaque extraction, puis ajouter des tests et des exports depuis l'application.

## Auteurs

Projet académique réalisé par **Can Pekgoz** et **Vanilla Nirinah Rafidison**.
