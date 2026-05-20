# Stock Revenue Dashboard

A Python-based data analysis and visualization project that combines historical stock price data with company revenue data to create interactive dashboards.

## Overview

This project extracts stock market data using the `yfinance` library and web scrapes revenue data from online sources. It then visualizes the relationship between stock prices and company revenue over time using interactive Plotly charts.

## Features

- **Stock Data Extraction**: Retrieve complete historical stock price data using yfinance API
- **Revenue Data Extraction**: Web scrape revenue data from HTML tables
- **Data Processing**: Clean and format data for analysis
- **Interactive Dashboards**: Visualize stock prices and revenue trends with Plotly
- **Multi-stock Support**: Analyze multiple companies (Tesla, GameStop, etc.)

## Project Structure

```
Stock_Revenue_Dashboard/
├── Stock_Revenue_Dashboard (1).ipynb    # Main Jupyter notebook
└── README.md                             # Project documentation
```

## Requirements

Make sure you have the following Python libraries installed:

```
yfinance
pandas
plotly
```

### Installation

```bash
pip install yfinance pandas plotly
```

## Usage

### 1. Extract Stock Data

Use the `extract_stock_data()` function to retrieve historical stock prices:

```python
from Stock_Revenue_Dashboard import extract_stock_data

# Get Tesla stock data
tesla_stock_data = extract_stock_data("TSLA")
print(tesla_stock_data.head())
```

Returns a DataFrame with columns: `Date`, `Open`, `High`, `Low`, `Close`, `Volume`

### 2. Extract Revenue Data

Use the `extract_revenue_data_from_url()` function to web scrape revenue data:

```python
from Stock_Revenue_Dashboard import extract_revenue_data_from_url

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
revenue_data = extract_revenue_data_from_url(url)
print(revenue_data.head())
```

Returns a DataFrame with columns: `Date`, `Revenue`

### 3. Create Dashboard

Generate an interactive dashboard combining stock and revenue data:

```python
from Stock_Revenue_Dashboard import create_dashboard

# Create Tesla dashboard
create_dashboard(tesla_stock_data, tesla_revenue_data, "Tesla Stock and Revenue Dashboard")
```

## Examples

### Tesla Analysis

```python
# Extract Tesla stock data
tesla_stock_data = extract_stock_data("TSLA")

# Extract Tesla revenue data
tesla_revenue_url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/revenue.htm"
tesla_revenue_data = extract_revenue_data_from_url(tesla_revenue_url)

# Create dashboard
create_dashboard(tesla_stock_data, tesla_revenue_data, "Tesla Stock and Revenue Dashboard")
```

### GameStop Analysis

```python
# Extract GameStop stock data
gme_stock_data = extract_stock_data("GME")

# Extract GameStop revenue data
gme_revenue_url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"
gme_revenue_data = extract_revenue_data_from_url(gme_revenue_url)

# Create dashboard
create_dashboard(gme_stock_data, gme_revenue_data, "GameStop Stock and Revenue Dashboard")
```

## Functions

### `extract_stock_data(ticker: str) -> pd.DataFrame`

Extracts historical stock data for a given ticker symbol.

**Parameters:**
- `ticker` (str): Stock ticker symbol (e.g., "TSLA", "GME")

**Returns:**
- DataFrame with columns: `Date`, `Open`, `High`, `Low`, `Close`, `Volume`

---

### `extract_revenue_data_from_url(url: str) -> pd.DataFrame`

Web scrapes revenue data from an HTML URL containing a financial table.

**Parameters:**
- `url` (str): URL containing the revenue data HTML table

**Returns:**
- DataFrame with columns: `Date`, `Revenue` (cleaned and formatted as float)

**Data Processing:**
- Removes NaN values
- Filters out "-" entries
- Removes currency symbols and commas
- Converts dates to datetime format

---

### `create_dashboard(stock_df: pd.DataFrame, revenue_df: pd.DataFrame, title: str)`

Creates an interactive Plotly dashboard combining stock and revenue data.

**Parameters:**
- `stock_df` (pd.DataFrame): Stock data with `Date` and `Close` columns
- `revenue_df` (pd.DataFrame): Revenue data with `Date` and `Revenue` columns
- `title` (str): Dashboard title

**Features:**
- Dual-axis visualization (Stock Price & Revenue)
- Interactive legend
- Range slider for date selection
- Hover tooltips with data values

## Data Sources

- **Stock Data**: Retrieved via yfinance API (Yahoo Finance)
- **Revenue Data**: Web scraped from IBM Developer Skills Network cloud storage

## Output

The dashboard displays:
- **Stock Price** (in USD): Line chart of closing prices over time
- **Revenue** (in millions USD): Line chart of quarterly/annual revenue
- **Interactive Features**: 
  - Zoom and pan capabilities
  - Legend toggle for data series
  - Date range slider
  - Hover information

## Notes

- Stock data is retrieved with the maximum available history for the ticker
- Revenue data requires clean HTML table formatting with Date and Revenue columns
- All revenue values are converted to numeric format (currency symbols removed)
- Dashboard uses Plotly for interactive visualizations

## License

This project is provided as-is for educational purposes.

## Contributing

Feel free to fork, modify, and enhance this project. Some potential improvements:

- Add more technical indicators (Moving Averages, RSI, etc.)
- Support for multiple currencies
- Export dashboard as HTML file
- Add statistical correlation analysis between stock price and revenue
- Support for real-time data updates

## Troubleshooting

**Issue: yfinance connection error**
- Solution: Check your internet connection and ensure yfinance servers are accessible

**Issue: Revenue data parsing error**
- Solution: Verify the URL contains a properly formatted HTML table with Date and Revenue columns

**Issue: Plotly not displaying**
- Solution: Ensure you're running in a Jupyter notebook or use `fig.show()` explicitly

---

**Last Updated**: 2026-05-20

For questions or issues, please open an issue on the GitHub repository.
