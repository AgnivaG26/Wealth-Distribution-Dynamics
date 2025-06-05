# Wealth Distribution Dynamics
## Overview

This project gives an introduction to wealth distribution dynamics, with a focus on
- modeling and computing the wealth distribution via simulation,  
- measures of inequality such as the Lorenz curve and Gini coefficient, and  
- how inequality is affected by the properties of wage income and returns on assets.

One interesting property of the wealth distribution we discuss is Pareto tails. For a review of the empirical evidence, see, for example, [[Benhabib and Bisin, 2018 (https://python.quantecon.org/zreferences.html#id71)].  

This is consistent with high concentration of wealth amongst the richest households.

It also gives us a way to quantify such concentration, in terms of the tail index.
One question of interest is whether or not we can replicate Pareto tails from a relatively simple model.

### Assumptions
The evolution of wealth for any given household depends on their savings behavior. Modeling such behavior will form an important part of this project. Here, we explore a rather ad hoc (but plausible) savings rule. 

We do this to more easily explore the implications of different specifications of income dynamics and investment returns.

At the same time, all of the techniques discussed here can be plugged into models that use optimization to obtain savings rules.

## Lorenz Curves and Gini Coefficient
Before we investigate wealth dynamics, we briefly review some measures of inequality.

### Lorenz Curves
One popular graphical measure of inequality is the [Lorenz curve](https://en.wikipedia.org/wiki/Lorenz_curve).

The package [QuantEcon.py](https://github.com/QuantEcon/QuantEcon.py), which we have used in this project, contains a function to compute Lorenz curves.

### The Gini Coefficient

The definition and interpretation of the Gini coefficient can be found on the corresponding [Wikipedia page](https://en.wikipedia.org/wiki/Gini_coefficient).

A value of 0 indicates perfect equality (corresponding the case where the Lorenz curve matches the 45 degree line) and a value of 1 indicates complete
inequality (all wealth held by the richest household).

The [QuantEcon.py](https://github.com/QuantEcon/QuantEcon.py) library contains a function to calculate the Gini coefficient.

## A Model of Wealth Dynamics
Having discussed inequality measures, let us now turn to wealth dynamics.

The model we will study is
```math
w_{t+1} = (1 + r_{t+1}) s(w_t) + y_{t+1}
```
where
- $w_t$ is wealth at time $t$ for a given household,  
- $r_t$ is the rate of return of financial assets,  
- $y_t$ is current non-financial (e.g., labor) income, and  
- $s(w_t)$ is current wealth net of consumption

Letting $\{z_t\}$ be a correlated state process of the form

```math
z_{t+1} = a z_t + b + \sigma_z \epsilon_{t+1}
```

we’ll assume that

```math
R_t := 1 + r_t = c_r \exp(z_t) + \exp(\mu_r + \sigma_r \xi_t)
```
and

```math
y_t = c_y \exp(z_t) + \exp(\mu_y + \sigma_y \zeta_t)
```
Here $\{ (\epsilon_t, \xi_t, \zeta_t) \}$ is IID and standard normal in $\mathbb{R}^3$.

The value of $c_r$ should be close to zero, since rates of return on assets do not exhibit large trends.

When we simulate a population of households, we will assume all shocks are idiosyncratic (i.e.,  specific to individual households and independent across them).

Regarding the savings function $s$, our default model will be

```math
s(w) = s_0 w \cdot \mathbb{1}\{w \geq \hat{w}\} 
```

where $s_0$ is a positive constant.

Thus, for $w < \hat{w}$, the household saves nothing. For  $w \geq \bar{w}$, the household saves a fraction $s_0$ of their wealth.

We are using something akin to a fixed savings rate model, while acknowledging that low wealth households tend to save very little.

##Applications

We simulate the model at different parameter values and investigate the implications for the wealth distribution. We take a look at the wealth dynamics for an individual household from a Time Series perspective.

We also generate a cross section sample, compute the Lorenz and Gini coefficients, and look at how inequaliy varies with returns on financial assets.

