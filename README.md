# Crypto Token Correlation Heatmap

This project analyzes the correlation and volatility of selected crypto tokens using historical price data from the CoinGecko Pro API. It visualizes token correlations as a heatmap and computes volatility for each token.

## Features

- **Fetch historical price data** for multiple tokens via CoinGecko Pro API.
- **Save and load price data** using `joblib` for efficient reuse.
- **Calculate log returns** and **volatility** for each token.
- **Visualize token correlations** with a heatmap using Seaborn and Matplotlib.

## Setup

1. **Clone the repository** and navigate to the project folder.

2. **Install dependencies:**
    ```
    pip install -r requirements.txt
    ```

3. **Set up your CoinGecko Pro API key:**
    - Create a `.env` file in the project root:
      ```
      GECKO_API=your_actual_api_key_here
      ```

## Usage

1. **Fetch and save token price data:**
    - Run the notebook or script that calls the CoinGecko API and saves the DataFrame with `joblib`.

2. **Analyze correlations and volatility:**
    - Open `tokens_correl.ipynb`.
    - Load the saved DataFrame.
    - Compute log returns and volatility.
    - Plot the correlation heatmap.

## Example

```python
import joblib
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np

# Load saved price data
df_prices_loaded = joblib.load("Database/df_prices.joblib")

# Calculate log returns
returns = df_prices_loaded.pct_change().apply(lambda x: np.log1p(x))

# Correlation matrix
corr = returns.corr()

# Plot heatmap
plt.figure(figsize=(8, 6))
sns.heatmap(corr, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.title("Token Correlation Heatmap")
plt.show()
```

## Output

- **Correlation heatmap** showing relationships between token returns.
- **Volatility values** for each token.

## Notes

- Ensure your API key is valid and correctly set in `.env`.
- Data is saved in the `Database` folder for reuse.
- You can customize the list of tokens and time period in the data fetching script.

##