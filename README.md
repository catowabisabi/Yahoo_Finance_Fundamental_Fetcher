# Yahoo Finance Fundamental Fetcher

A tool to fetch comprehensive fundamental and market data from Yahoo Finance using the yfinance library.

一個使用 yfinance 函式庫從雅虎財經（Yahoo Finance）抓取全面基本面與市場數據的工具。

## 📖 Introduction / 簡介

### English
This project provides a powerful and reliable script to download a wide range of financial data for publicly traded companies directly from Yahoo Finance. By leveraging the yfinance library, it offers a stable and easy-to-use interface for programmatic access to financial statements, market data, and company information.

### 中文 (繁體)
這個專案提供了一個強大且可靠的腳本，用於從雅虎財經直接下載上市公司的多種類型財務數據。透過利用 yfinance 函式庫，它為程式化獲取財務報表、市場數據和公司資訊提供了一個穩定且易於使用的介面。

## 🎯 Purpose / 用途

### English
The primary goal is to automate and simplify the data collection process for in-depth financial analysis, quantitative modeling, or academic research. Instead of relying on brittle web scrapers, this tool uses a robust library to quickly fetch and save consistent, structured data for multiple tickers.

### 中文 (繁體)
此工具的主要目標是自動化並簡化數據收集流程，以進行深入的財務分析、量化模型建立或學術研究。它不依賴脆弱的網路爬蟲，而是使用一個功能強大的函式庫，來快速抓取並保存多個股票代碼的一致性、結構化數據。

## ✨ Features / 主要功能

Based on the yfinance library, this tool can fetch a comprehensive set of data.

基於 yfinance 函式庫，本工具可抓取一套全面的數據。

| Data Category / 數據類別 | English | 中文 (繁體) |
|-------------------------|---------|-------------|
| Company Info | info, sustainability, recommendations, calendar, isin, news | 公司基本資訊、永續性報告 (ESG)、分析師建議、活動日曆、國際證券識別碼、相關新聞 |
| Market Data | history, actions (dividends, splits), options | 歷史股價、公司行動 (股息、股票分割)、選擇權鏈 |
| Financial Statements | financials (annual), quarterly_financials | 年度財務報表、季度財務報表 |
| Balance Sheet | balance_sheet (annual), quarterly_balance_sheet | 年度資產負債表、季度資產負債表 |
| Cash Flow | cashflow (annual), quarterly_cashflow | 年度現金流量表、季度現金流量表 |
| Ownership | major_holders, institutional_holders | 主要股東、機構持股人 |

## ⚙️ Installation / 安裝

**Clone the repository: / 克隆儲存庫：**

```bash
git clone https://github.com/catowabisabi/Yahoo_Finance_Fundamental_Fetcher.git
cd Yahoo_Finance_Fundamental_Fetcher
```

**Install dependencies: / 安裝依賴套件：**

The project requires yfinance for data fetching and pandas for data handling.

```bash
pip install yfinance pandas
```

## 🚀 Usage / 使用方法

### English
You can use the yfinance library in your Python script to fetch the desired data. Create a .py file and use the following code structure as a guide. The fetched data, which is a pandas DataFrame, can be easily saved to a CSV file.

### 中文 (繁體)
您可以在您的 Python 腳本中使用 yfinance 函式庫來獲取所需數據。建立一個 .py 檔案，並使用以下程式碼結構作為指南。抓取到的數據是一個 pandas DataFrame，可以輕鬆地存為 CSV 檔案。

### Example Script / 範例腳本 (main.py):

This example shows how to fetch the annual financial statements for Apple (AAPL) and save them to a file.

此範例展示了如何抓取蘋果公司（AAPL）的年度財務報表並將其存檔。

```python
import yfinance as yf
import os

# List of stock tickers you want to fetch
tickers = ["AAPL", "MSFT", "GOOGL"]

# Create an 'output' directory if it doesn't exist
output_dir = 'output'
if not os.path.exists(output_dir):
    os.makedirs(output_dir)

# Loop through each ticker
for ticker_symbol in tickers:
    try:
        print(f"Fetching data for {ticker_symbol}...")
        
        # Get the ticker object
        stock = yf.Ticker(ticker_symbol)
        
        # --- Fetch Financials ---
        financials = stock.financials
        if not financials.empty:
            file_path = os.path.join(output_dir, f"{ticker_symbol}_financials.csv")
            financials.to_csv(file_path)
            print(f"  > Saved financials to {file_path}")

        # --- Fetch Balance Sheet ---
        balance_sheet = stock.balance_sheet
        if not balance_sheet.empty:
            file_path = os.path.join(output_dir, f"{ticker_symbol}_balance_sheet.csv")
            balance_sheet.to_csv(file_path)
            print(f"  > Saved balance sheet to {file_path}")
            
        # --- Fetch Other Data (Example: Company Info) ---
        # info = stock.info 
        # print(f"  > Company Name: {info.get('longName')}")

    except Exception as e:
        print(f"Could not fetch data for {ticker_symbol}: {e}")

print("\nProcess complete.")
```

### How to Run / 如何執行:

Save the code above as main.py and run it from your terminal:

將以上程式碼儲存為 main.py 並從您的終端機執行：

```bash
python main.py
```

### Output / 輸出:

The script will create an output folder and save the financial data for each specified ticker into its own CSV file (e.g., AAPL_financials.csv, MSFT_balance_sheet.csv, etc.).

腳本將會建立一個 output 資料夾，並將每個指定股票的財務數據儲存到其各自的 CSV 檔案中（例如 AAPL_financials.csv、MSFT_balance_sheet.csv 等）。
