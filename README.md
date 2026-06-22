# EDS d'Ornstein-Uhlenbeck — Simulation & validation

Projet de finance quantitative. On y étudie le processus
d'Ornstein-Uhlenbeck (OU), un processus à retour à la moyenne très utilisé en finance
(taux d'intérêt, *pair trading*, modèle de Vasicek). L'objectif est de **simuler l'EDS
numériquement** et de **confronter les résultats aux formules théoriques** établies à la main
(espérance et variance).

## Le modèle

Le processus est défini par l'équation différentielle stochastique :

$$dX_t = a(\theta - X_t)\,dt + \sigma\,dB_t$$

- $a$ : vitesse de retour à la moyenne (*mean reversion rate*) ;
- $\theta$ : moyenne de long terme (cible) ;
- $\sigma$ : volatilité ;
- $B_t$ : mouvement brownien standard.

Solutions théoriques :

$$\mathbb{E}[X_t] = x_0 e^{-at} + \theta\,(1 - e^{-at})
\qquad
\mathbb{V}[X_t] = \frac{\sigma^2}{2a}\,(1 - e^{-2at})$$

Contrairement au mouvement brownien, la variance **sature** à $\sigma^2/2a$ : le processus
est stationnaire à long terme.

## Méthode

Schéma d'**Euler-Maruyama** vectorisé sur l'ensemble des trajectoires :

$$X_{t+1} = X_t + a(\theta - X_t)\,\Delta t + \sigma\sqrt{\Delta t}\,Z,
\qquad Z \sim \mathcal{N}(0,1)$$

On simule `n_sims = 2000` trajectoires, puis on compare moyenne et variance **empiriques**
(à chaque instant) aux formules théoriques. L'écart maximal est mesuré explicitement
pour valider les calculs de façon quantitative et pas seulement visuelle.

## Contenu du dépôt

| Fichier | Description |
|---|---|
| `EDS_Ornstein_Uhlenbeck.ipynb` | Notebook de simulation, visualisation et validation. |
| `EDS - Ornstein_Uhlenbeck.pdf`  | Rapport : résolution analytique de l'EDS (calculs manuscrits). |

## Exécution

```bash
conda create -n ou python=3.12 numpy matplotlib jupyter
conda activate ou
jupyter notebook EDS_Ornstein_Uhlenbeck.ipynb
```

## Auteur

**Rayane Ferrat** — ENSEIRB-MATMECA.
