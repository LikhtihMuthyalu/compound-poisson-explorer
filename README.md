## compound-poisson-explorer 💡

### Compound Poisson Process Sensitivity Analyzer using R Shiny

This project features an interactive R Shiny application that simulates and visualizes the **Compound Poisson Process (CPP)**, $S(t) = \sum_{i=1}^{N(t)} X_i$. It is designed to help users understand the sensitivity of the process's path and terminal distribution to changes in the key parameters: the arrival rate ($\lambda$) and the jump size rate ($\mu$).

-----

## 🔍 Mathematical Background

The Compound Poisson Process (CPP) modeled here is fundamental in areas like ruin theory (insurance/risk), queueing theory, and stochastic modeling.

### Process Definition:

$$S(t) = \sum_{i=1}^{N(t)} X_i$$

Where:

  * **$N(t)$ (Number of Jumps):** A **Poisson Process** with rate $\lambda$. This governs the *frequency* of the jumps (arrivals). Since the inter-arrival times are exponential, the number of events in a fixed interval $t$ is Poisson distributed, $N(t) \sim \text{Poisson}(\lambda t)$.
  * **$X_i$ (Jump Size/Claim Size):** Independent and identically distributed (i.i.d.) **Exponential random variables** with rate $\mu$. This governs the *magnitude* of the jumps. $X_i \sim \text{Exponential}(\mu)$.

### Key Analytical Results:

The application displays the theoretical mean and variance, which are directly impacted by the input parameters:

  * **Expected Value at time $t$:**
    $$E[S(t)] = E[N(t)] \cdot E[X] = (\lambda t) \cdot (1/\mu)$$
  * **Variance at time $t$:**
    $$\text{Var}[S(t)] = \text{Var}[N(t)] E[X]^2 + E[N(t)] \text{Var}[X] = \lambda t \cdot \frac{2}{\mu^2}$$

-----

## 🛠️ Installation and Usage

### Prerequisites

You need **R** and the following R packages installed:

  * `shiny`
  * `ggplot2`

You can install them from your R console:

```r
install.packages(c("shiny", "ggplot2"))
```

### usinging the Application

1.  **use the R Shinyapps.io link:**

```bash
https://transition-probability-matrix.shinyapps.io/CPPSimulation/
```
-----

## ⚙️ Application Features

The R Shiny interface provides two main tabs for sensitivity analysis:

### 1\. Process Path $S(t)$ vs Time

  * **Function:** Displays a **single realization** (a sample path) of the Compound Poisson Process $S(t)$ over the maximum time $T$.
  * **Sensitivity Insight:**
      * **Increase $\lambda$**: The path shows more **frequent** jumps.
      * **Decrease $\mu$**: The path shows **larger** jumps (since $E[X] = 1/\mu$).

### 2\. Final Distribution Histogram

  * **Function:** Plots a histogram of $S(T)$ generated from a high number of simulations ($N_{\text{sim}}$) at the fixed final time $T$.
  * **Sensitivity Insight:**
      * **Increase $\lambda$ or Decrease $\mu$**: The distribution shifts **right** (higher mean) and becomes **wider** (higher variance).
      * **Large $T$**: The histogram will increasingly resemble a **Normal Distribution** due to the Central Limit Theorem (CLT) applied to the random sum of the $X_i$'s.

-----

## 📄 Code Structure

The application logic is contained within `app.R` and includes:

  * **`simulate_cpp_path(lambda, mu, T_max)`:** Simulates a single, time-indexed path and structures the data for a step-function plot.
  * **`simulate_cpp_final_values(lambda, mu, T_max, N_simulations)`:** Simulates the final value $S(T)$ for many iterations to generate the distribution data.
  * **`ui` (User Interface):** Defines the sliders for $\lambda$, $\mu$, and $T$, and the action button.
  * **`server` (Backend Logic):** Handles the reactive simulation, plotting using `ggplot2`, and calculation of the theoretical moments $E[S(T)]$ and $\text{Var}[S(T)]$.

-----

## 🖋️ Author

Likhith G Muthyalu


