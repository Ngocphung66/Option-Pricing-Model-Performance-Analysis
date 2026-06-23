# Option Pricing Model Comparison

A derivatives research project that compares **Machine Learning**, **Black–Scholes**, **Monte Carlo Simulation**, and the **Binomial Tree Method** for pricing vanilla call and put options.

The project combines financial theory, numerical methods, machine-learning regression, historical backtesting, and interactive visualization. Its main objective is to compare the models in terms of **pricing accuracy, interpretability, convergence, flexibility, and computational performance**.

---

## Research Questions

- How closely does each model estimate observed market option prices?
- How do volatility, moneyness, and time to maturity affect pricing error?
- How quickly does Monte Carlo pricing converge?
- Can machine-learning regression improve pricing accuracy relative to traditional benchmarks?
- What are the strengths and limitations of each approach?

---

## Models

### Machine Learning

Regression models such as **XGBoost** and **Random Forest** estimate option prices from features including:

- Underlying stock price
- Strike price
- Time to maturity
- Risk-free rate
- Historical or implied volatility
- Option type

### Black–Scholes

A closed-form benchmark for European-style options under assumptions such as constant volatility, continuous trading, and lognormal stock-price dynamics.

### Monte Carlo Simulation

Simulates future stock-price paths under Geometric Brownian Motion and estimates the discounted expected payoff. The implementation includes convergence analysis, simulated paths, and payoff distributions.

### Binomial Tree

Models discrete upward and downward price movements and calculates the option value through backward induction under risk-neutral probabilities.

---

## Key Features

- Supports **user-selected equity tickers** through `yfinance`
- Prices both **call and put options**
- Implements:
  - Machine Learning regression
  - Black–Scholes
  - Monte Carlo Simulation
  - Binomial Tree
- Performs historical option-pricing backtests
- Calculates historical volatility from daily returns
- Estimates implied volatility from market prices
- Computes **Delta, Gamma, Vega, Theta, and Rho**
- Generates automated text reports
- Produces model-comparison and sensitivity visualizations

---

## Data

Historical backtesting uses **AAPL option data from 2013**, sourced from [OptionData.org](https://optiondata.org/).

Underlying equity data is retrieved through Yahoo Finance using `yfinance`. The interface supports different stock tickers, allowing the pricing workflow to be applied across multiple equities.

> Yahoo Finance data is used for research and demonstration purposes and should not be treated as exchange-grade real-time data.

---

## Inputs

| Input | Description |
|---|---|
| Stock ticker | Equity symbol such as `AAPL` or `MSFT` |
| Stock price | Current underlying price |
| Strike price | Option exercise price |
| Days to expiration | Remaining option life |
| Risk-free rate | Annualized rate |
| Market option price | Used to estimate implied volatility |
| Option type | Call or put |
| Historical period | Used to estimate volatility |
| Monte Carlo simulations | Number of simulated paths |
| Binomial steps | Number of tree steps |

---

## Outputs

The application generates:

- Option prices from each model
- Historical and implied volatility
- Option Greeks
- Automated `options_report.txt`
- Model-comparison plots
- Option price versus stock price
- Monte Carlo paths
- Payoff distribution
- Monte Carlo convergence
- Historical backtesting charts

---

## Sample Performance

The following example compares model prices with an observed market price of **22.25**.

| Model | Estimated Price | Absolute Error | Percentage Error |
|---|---:|---:|---:|
| Monte Carlo | 19.24 | 3.01 | 13.53% |
| Black–Scholes | 19.17 | 3.08 | 13.84% |
| Binomial Tree | 19.17 | 3.08 | 13.84% |

In this individual scenario, Monte Carlo produced the lowest pricing error. This is a **single valuation example**, not a full-sample performance conclusion.

### Sample Greeks

| Greek | Value |
|---|---:|
| Delta | 0.9983 |
| Gamma | 0.0008 |
| Vega | 0.1710 |
| Theta | -11.3226 |
| Rho | 3.9682 |

The sample historical volatility was **21.91%**, while the implied volatility derived from the observed option price was **82.16%**.

---

## Performance Evaluation

A full backtest should compare models using:

- **MAE**
- **RMSE**
- **MAPE**
- **R²** for machine-learning models
- Execution time
- Monte Carlo convergence error
- Pricing error by:
  - Moneyness
  - Time to maturity
  - Volatility regime
  - Call versus put

Chronological train-validation-test splits should be used to reduce look-ahead bias.

---

## Visual Examples

### Historical Backtesting

<img width="3600" height="1800" alt="image" src="https://github.com/user-attachments/assets/b056fd64-1a63-4c25-8a3a-55c5d1cacdd3" />


### Option Price Sensitivity

<img width="3600" height="1800" alt="image" src="https://github.com/user-attachments/assets/37587e9a-8c8e-41bb-a86f-c53f2c83ab16" />


### Monte Carlo Paths

<img width="3600" height="1800" alt="image" src="https://github.com/user-attachments/assets/d069235a-19fc-4caf-b15b-27ce8c04eac7" />

### Monte Carlo Convergence

<img width="3600" height="1800" alt="image" src="https://github.com/user-attachments/assets/9a3f8669-01d1-4b07-8bda-f00b5b9638bc" />


---

## Installation

Python **3.11 or 3.12** is recommended.

```bash
git clone <your-repository-url>
cd <repository-folder>

python -m venv venv
```

Activate the environment:

```bash
# macOS/Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Run the Project

### Streamlit Application

```bash
streamlit run option_pricing_app.py
```

The application normally opens at:

```text
http://localhost:8501
```

### Python Script

```bash
python src/main.py
```

### Jupyter Notebook

Open:

```text
src/main.ipynb
```

---

## Main Parameters

| Parameter | Description |
|---|---|
| `ticker` | Equity ticker |
| `K` | Strike price |
| `T` | Time to maturity |
| `r` | Annualized risk-free rate |
| `mc_num_sim` | Number of Monte Carlo simulations |
| `bt_num_step` | Number of Binomial Tree steps |

---

## Limitations

- Black–Scholes assumes constant volatility and continuous trading
- Historical volatility may differ substantially from forward-looking implied volatility
- Monte Carlo results contain simulation error
- Binomial estimates depend on the number of steps
- Machine-learning models may overfit historical observations
- Market prices may be affected by liquidity and bid–ask spreads
- Dividends, transaction costs, and early exercise may require additional modeling
- The lowest in-sample error does not guarantee the best out-of-sample performance

This repository is intended for **research and educational purposes** and does not provide investment advice.

---

## Future Improvements

- Add walk-forward and out-of-sample validation
- Report MAE, RMSE, MAPE, and runtime for every model
- Evaluate performance by moneyness and maturity bucket
- Add dividend-yield adjustments
- Estimate a volatility surface
- Support American-option exercise
- Add stochastic-volatility and jump-diffusion models
- Add feature-importance or SHAP analysis
- Expand backtesting to more equities and market regimes


