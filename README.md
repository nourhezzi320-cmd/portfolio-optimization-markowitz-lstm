# Optimisation de Portefeuille : Markowitz + Deep Learning (LSTM/BiLSTM)

Projet combinant optimisation convexe classique et apprentissage profond pour la sélection de portefeuille, appliqué à un univers d'investissement réel mixte (actions américaines + actions tunisiennes cotées à la BVMT).

**[Lire le livre complet (PDF)](./book/main.pdf)**

## Contexte

Ce projet formalise le modèle de Markowitz (1952) comme un programme d'optimisation quadratique convexe, dérive sa solution analytique via les conditions de Karush-Kuhn-Tucker, puis étend le modèle classique à l'aide de réseaux de neurones récurrents (BiLSTM) pour la prévision des rendements — avec une validation empirique rigoureuse à chaque étape.

## Résultats clés

| Résultat | Valeur |
|---|---|
| Sharpe in-sample (modèle classique) | 6.23 |
| Sharpe out-of-sample (modèle classique) | **-0.35** |
| Sharpe out-of-sample (augmenté ML) | **-0.27** |
| Significativité de l'écart (bootstrap, 5000 tirages) | Non concluante (IC 90% inclut 0) |

Le point central du projet : un ratio de Sharpe in-sample excellent ne garantit **aucunement** une performance future — la validation out-of-sample est non négociable.

## Structure du dépôt

```
├── book/
│   ├── main.pdf              # Le livre complet
│   ├── main.tex               # Fichier LaTeX principal
│   ├── chapitre1.tex … chapitre8.tex
│   └── references.bib         # Bibliographie (11 sources)
├── code/
│   ├── portfolio_optimization.py   # Chapitres 3-4 : Markowitz + backtest
│   ├── lstm_prediction.py          # Chapitre 5 : prévision BiLSTM
│   ├── chapitre6_ml_portfolio.py   # Chapitre 6 : portefeuille augmenté ML
│   └── chapitre7_analyse.py        # Chapitre 7 : MDD, VaR, bootstrap
├── figures/
│   └── *.png                  # Toutes les figures générées
└── README.md
```

## Méthodologie (résumé des chapitres)

1. **Théorie** — Formalisation du modèle de Markowitz, dérivation des conditions KKT
2. **Données réelles** — Actions US (yfinance) + BVMT (BIAT, BT, SFBT), frontière efficiente
3. **Estimation risk** — Validation out-of-sample révélant l'effondrement du Sharpe
4. **Deep Learning** — BiLSTM pour la prévision des rendements (résultats honnêtes : R² négatif)
5. **Portefeuille augmenté ML** — Intégration des prévisions dans l'optimisation
6. **Comparaison rigoureuse** — MDD, VaR, test de significativité par bootstrap

## Technologies utilisées

- **Python** : numpy, pandas, scipy (optimisation QP), scikit-learn, TensorFlow/Keras
- **Data** : yfinance (actions US), ilboursa.com (actions BVMT)
- **LaTeX** : rédaction du livre complet

## Reproduire les résultats

```bash
pip install -r requirements.txt
python code/portfolio_optimization.py   # Chapitres 3-4
python code/lstm_prediction.py          # Chapitre 5
python code/chapitre6_ml_portfolio.py   # Chapitre 6
python code/chapitre7_analyse.py        # Chapitre 7
```

*Note : les données BVMT (BIAT.csv, BT.csv, SFBT.csv) ne sont pas incluses (à obtenir manuellement via ilboursa.com, voir Chapitre 3 du livre).*

## Auteur

[Ton Nom] — [ton lien LinkedIn]
