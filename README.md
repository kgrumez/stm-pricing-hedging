# Pricing, volatilité de marché et couverture dynamique — STMicroelectronics

**Problème.** Peut-on aller au-delà de la théorie du pricing d'options (Black-Scholes, 
Monte-Carlo) et la confronter à un vrai marché ? Ce projet part du pricing académique, 
le teste contre la volatilité implicite réelle de STM (NYSE), l'applique à un payoff 
structuré (Autocall), puis simule et backteste la couverture dynamique d'une position 
vendeuse — le cœur du métier de market-maker.

**Méthode.** Pricers Black-Scholes fermé et Monte-Carlo (convergence validée), 
volatilité historique vs implicite (IV recalculée par inversion BS, les champs Yahoo 
étant peu fiables sur ce sous-jacent), Autocall Phoenix pricé et calibré au pair 
(coupon 16,09%), delta-hedging quotidien simulé (5 000 trajectoires) puis backtesté 
sur l'historique réel de STM.

**Résultat clé.** Vendre à IV (56,4%) et couvrir alors que la vol réalisée est plus 
basse (47,6%) génère un P&L moyen de +0,93€ (98,2% de scénarios gagnants) — le mécanisme 
classique du vol trading, confirmé en direction sur données réelles (16 fenêtres, 
P&L moyen +0,36€, 75% de fenêtres gagnantes).

**Limite.** Le backtest réel repose sur seulement 16 fenêtres indépendantes 
(5 ans d'historique / 77 jours par fenêtre) — l'intervalle de confiance à 95% inclut 0. 
Le mécanisme est confirmé en direction, pas en précision statistique.

## Résultats visuels
- `fig1_convergence_mc_bs.png` — convergence Monte-Carlo vers Black-Scholes
- `fig2_term_structure_iv.png` — term structure de l'IV vs vol réalisée
- `fig3_hedge_pnl_iv_high.png` / `fig4_hedge_pnl_iv_low.png` — P&L de hedge, IV>RV et RV>IV
- `fig5_hedge_threshold_arbitrage.png` — arbitrage coûts de transaction vs qualité de couverture

## Structure du repo
- `pricing_hedging_stm.ipynb` — notebook complet (Phases 1 à 6)
- `fig*.png` — graphiques ci-dessus
- `README.md` — ce fichier

## Stack
Python · numpy · scipy · pandas · matplotlib · yfinance
