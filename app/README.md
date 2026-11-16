# Application Google Trends

L'application Streamlit permet d'explorer les séries temporelles et les indices géographiques préparés par le projet. Son code se trouve dans [`streamlit_app.py`](streamlit_app.py).

[Présentation du projet](../README.md) | [Données préparées](../data/processed/) | [Scripts de traitement](../scripts/)

## Démarrage

Depuis la racine du dépôt, avec un environnement Python activé :

```bash
python -m pip install -r requirements.txt
python -m streamlit run app/streamlit_app.py
```

L'adresse locale habituelle est `http://localhost:8501`. Les fichiers préparés sont présents dans le dépôt ; une nouvelle collecte n'est pas nécessaire pour consulter cette version.

## Fichiers attendus

Le script construit les chemins à partir de son emplacement, puis lit les fichiers dans `data/processed/`.

| Fichier | Contenu utilisé |
|---|---|
| `trends_time_long.csv` | Date, mot-clé et indice temporel |
| `trends_country_enriched.csv` | Pays, continent, code ISO3, mot-clé et indice géographique |
| `country_insights.csv` | Mot-clé sélectionné par l'algorithme, deux meilleurs indices et leur écart |

La fonction `load_data`, mise en cache avec `st.cache_data`, charge les fichiers et vérifie les colonnes attendues. Certaines conversions numériques remplacent les valeurs invalides par zéro : ce traitement doit être pris en compte dans l'interprétation.

## Navigation

| Onglet | Contenu |
|---|---|
| Vue générale | Séries temporelles, indicateurs et comparaison par continent |
| Carte et pays | Carte mondiale, classement des pays et nuage de points |
| Comparaisons | Distributions, matrice pays et mots-clés, profils comparés |
| Résumé et données | Commentaire calculé à partir des filtres et consultation des tableaux |

La barre latérale propose le choix du mot-clé, des continents, de la métrique, du nombre de pays et d'un seuil minimum. Les commentaires proviennent de calculs déterministes, sans modèle de langage.

## Lecture des métriques

| Libellé de l'interface | Calcul | Interprétation |
|---|---|---|
| « Score absolu » | Indice Google Trends d'origine | Indice relatif fourni par Google, jamais un volume de recherches |
| « Score normalisé » | `(score - min) / (max - min) * 100` | Nouvelle échelle entre les extrêmes du sous-ensemble utilisé |
| « Part du maximum (%) » | `score / score_max * 100` | Rapport au meilleur indice du sous-ensemble utilisé |

Les transformations supplémentaires modifient l'échelle d'affichage. Elles ne rendent pas comparables des séries issues d'extractions normalisées séparément.

## Limite des comparaisons entre mots-clés

Le script de collecte interroge les pays **séparément pour chaque mot-clé**. Les échelles obtenues sont propres à chaque extraction. Les cartes de « domination », classements entre mots-clés et écarts calculés sont exploratoires : ils ne permettent pas d'affirmer qu'un sujet est réellement plus recherché qu'un autre dans un pays.

Une comparaison de niveaux entre sujets demanderait une collecte sur une échelle commune. Les périodes temporelle et géographique sont également différentes. Voir les [périodes et limites du projet](../README.md#limites).

## Diagnostic

- Fichier absent : vérifier `data/processed/` ou régénérer les sorties dans l'ordre indiqué dans le README principal.
- Colonne manquante : vérifier que les fichiers correspondent aux sorties des scripts du dépôt.
- Carte incomplète : examiner les codes ISO3 et les métadonnées géographiques.
- Valeurs inattendues : vérifier les filtres, la métrique choisie et le traitement des valeurs manquantes.

Cette page documente le code disponible. Elle ne revendique pas une nouvelle exécution de l'application ni un déploiement public.
