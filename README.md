# Bayesian Causal Impact Analysis

This repository implements **Bayesian Structural Time-Series Models** to infer the causal impact of an intervention on time-series data. It follows the methodology outlined in [Brodersen et al. (2015)](https://doi.org/10.1214/14-AOAS788), where causal inference is achieved by estimating a counterfactual response using Bayesian state-space models.

By predicting what would have happened in the absence of an intervention and comparing this counterfactual with observed data, we accurately quantify **uplift effects** in synthetic datasets. Our implementation captures the cumulative impact of interventions while maintaining uncertainty quantification via posterior distributions.

## Mathematical Formulation

The model follows a **state-space representation**:

**Observation Equation**:

$$ y_t = Z_t^T \alpha_t + \epsilon_t, \quad \epsilon_t \sim N(0, \sigma^2) $$

**State Equation**:

$$ \alpha_{t+1} = T_t \alpha_t + R_t \eta_t, \quad \eta_t \sim N(0, Q_t) $$

where:
- \( y_t \) is the observed dependent variable,
- \( \alpha_t \) is the latent state vector,
- \( Z_t \) is the observation matrix,
- \( T_t \) is the transition matrix governing latent state evolution,
- \( R_t \) controls system noise,
- \( Q_t \) models latent state diffusion.

For causal impact estimation, we infer the counterfactual \( \tilde{y}_t \), then compute the **point-wise impact**:

$$ \delta_t = y_t - \tilde{y}_t $$

and **cumulative impact**:

$$ \Delta_T = \sum_{t=n+1}^{m} \delta_t $$

