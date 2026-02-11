---
title: "Analyse de la structure par terme de la volatilité : Les cryptomonnaies sont-elles mean-reverting ?"
date: 2026-02-11
draft: false
math: true
tags: ["crypto", "volatility", "hurst-exponent", "mean-reversion", "quantitative-analysis"]
categories: ["Quant Research"]
---

## Introduction

Dans le cadre du développement de stratégies de trading quantitatives sur les cryptomonnaies, une question fondamentale se pose : **les mouvements de prix sont-ils persistants (trend-following) ou mean-reverting ?**

Cette distinction est cruciale car elle détermine le type de stratégie à privilégier :
- **H > 0.5** : Persistance des mouvements → Stratégies trend-following
- **H = 0.5** : Marche aléatoire (mouvement brownien)
- **H < 0.5** : Retour à la moyenne → Stratégies mean-reverting

Dans cette étude, nous analysons la structure par terme de la volatilité de **164 paires de cryptomonnaies** sur l'année 2025 pour déterminer leur comportement caractéristique.

## Méthodologie

### Calcul de la volatilité multi-horizons

Pour chaque horizon temporel $T \in \{4h, 12h, 1j, 2.5j, 1s, 1m\}$, nous calculons la volatilité comme l'écart-type des log-rendements :

$$\sigma(T) = \sqrt{\frac{1}{N}\sum_{i=1}^N r_i^2}$$

où $r_i = \ln(P_{t+T} / P_t)$ sont les log-rendements.

### Exposant de Hurst

L'exposant de Hurst $H$ caractérise la persistance des mouvements de prix. Il est obtenu par régression linéaire sur la structure par terme de la volatilité :

$$\log(\sigma(T)) = \log(\sigma_0) + H \cdot \log(T)$$

**Interprétation** :
- $H = 0.5$ : Mouvement brownien (marche aléatoire)
- $H > 0.5$ : **Trend-following** (persistance des mouvements)
- $H < 0.5$ : **Mean-reverting** (retour à la moyenne)

### Code Python

```python
import numpy as np
import pandas as pd
from scipy.stats import linregress

def calculate_volatility(returns: pd.Series) -> float:
    """Calcule la volatilité (écart-type des rendements)."""
    return returns.std()

def calculate_hurst_exponent(volatilities: dict) -> float:
    """
    Calcule l'exposant de Hurst par régression log-log.
    
    Args:
        volatilities: Dict {timeframe_hours: volatility}
    
    Returns:
        Exposant de Hurst H
    """
    log_T = np.log([t for t in volatilities.keys()])
    log_sigma = np.log([v for v in volatilities.values()])
    
    slope, intercept, r_value, p_value, std_err = linregress(log_T, log_sigma)
    
    return slope  # H = slope de la régression
```

## Résultats

### Structure par terme de la volatilité

![Structure par terme de la volatilité](volatility_term_structure_all.png)

*Note : Graphique à ajouter depuis `python_utils/volatility_term_structure_all.png`*

### Distribution des exposants de Hurst

Sur 164 paires analysées :
- **Moyenne** : $H \approx 0.45$
- **Médiane** : $H \approx 0.46$
- **Écart-type** : $\sigma_H \approx 0.08$

**Conclusion préliminaire** : Les cryptomonnaies présentent un comportement **légèrement mean-reverting** en moyenne.

### Asymétrie hausse/baisse

Nous analysons également la persistance directionnelle pour comprendre si les hausses et les baisses se comportent différemment :

| Métrique | Valeur |
|----------|--------|
| $P(\uparrow \| \uparrow)$ | 48.2% |
| $P(\downarrow \| \downarrow)$ | 51.2% |
| **Asymétrie** | **+3.0%** |

**Observation clé** : Les baisses sont **plus persistantes** que les hausses, ce qui suggère que les mouvements baissiers ont tendance à se prolonger davantage.

## Discussion

### Paradoxe apparent

Nous observons un **paradoxe intéressant** :
1. L'exposant de Hurst $H < 0.5$ suggère un comportement mean-reverting
2. Mais l'asymétrie montre que les **baisses sont persistantes** ($P(\downarrow|\downarrow) > 50\%$)

### Interprétation

Ce paradoxe s'explique par la nature **multi-échelle** des marchés :
- **Court terme (4h-1j)** : Comportement mean-reverting dominant
- **Moyen terme (2-7j)** : Émergence de trends, notamment baissiers
- **Long terme (1m+)** : Retour à la moyenne

Les stratégies **short trend-following** sont donc particulièrement adaptées car elles :
1. Exploitent la persistance des mouvements baissiers
2. Bénéficient du mean-reversion pour les sorties de position

## Implications pour le trading

### Stratégies recommandées

1. **Short trend-following sur moyennes mobiles** :
   - Entrée : Croisement baissier de MA courte/longue
   - Sortie : Croisement haussier ou stop-loss
   - Horizon : 4h-1j

2. **Mean-reversion sur extrema** :
   - Entrée : Détection de sur-extension
   - Sortie : Retour à la moyenne mobile
   - Horizon : Intraday

### Gestion du risque

- **Stop-loss serré** : Le mean-reversion implique des reversals rapides
- **Position sizing adaptatif** : Réduire l'exposition sur faible volatilité
- **Hedge directionnel** : Couvrir les positions short en cas de rally

## Conclusion

Cette analyse de 164 paires de cryptomonnaies sur 2025 révèle :

1. ✅ Comportement **légèrement mean-reverting** ($H \approx 0.45$)
2. ✅ **Asymétrie baissière** : Les baisses sont plus persistantes (+3%)
3. ✅ Validation des stratégies **short trend-following**
4. ⚠️ Importance de la gestion du risque face au mean-reversion

### Perspectives

- Analyse par régimes de marché (bull/bear/sideways)
- Étude de la tail risk et des événements extrêmes
- Optimisation des horizons temporels par paire

## Code et données

Le code complet de cette analyse est disponible sur [GitHub](https://github.com/3edgesstrategy).

---

*Dernière mise à jour : Février 2026*
