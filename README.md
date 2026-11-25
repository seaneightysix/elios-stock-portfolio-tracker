# Elios Stock Portfolio Tracker

A single-user, local development version of the Elios Academy capstone. The first run seeds fictional AAPL and GOOGL positions across investment and retirement accounts. You can replace positions, record dated quotes, maintain favorites and request a saved portfolio analysis.

## Run on macOS in VS Code

Install Python 3.10 or newer, Git, VS Code and Microsoft's Python extension. The app uses the Python standard library. In Terminal:

```sh
git clone https://github.com/seaneightysix/elios-stock-portfolio-tracker.git
cd elios-stock-portfolio-tracker
python3 app.py
```

Open http://127.0.0.1:8765 in your browser. For debugging, open the cloned folder in VS Code, select a Python 3.10+ interpreter, choose **Run portfolio tracker** in Run and Debug, then press F5. Stop an existing terminal run with Ctrl+C before starting the debugger.

## Optional OpenAI analysis

The dashboard works offline. Clicking **Analyze portfolio** sends the displayed holding records, including account labels, and quote dates to OpenAI. The server reads OPENAI_API_KEY from its environment or a private .env.local file in the checkout. A key saved in a remote workspace does not accompany a Git clone. Set the credential separately on the computer running the app. The default model is gpt-4.1-mini. Set OPENAI_MODEL in the server environment to override it. Each click makes a billable request and saves a completed result. The dashboard shows the most recent successful analysis.

## Storage and calculations

SQLite stores holdings keyed by account and ticker, dated USD prices, favorites and analyses in portfolio.sqlite3 alongside the app. Back up this file while the app is stopped. The database and local environment files are ignored by Git. A holding stores shares and the average purchase price per share. Editing a holding replaces its quantity and average price. A quote applies to every holding of the same ticker. Cost basis is shares × average purchase price. Unrealized gain or loss is market value minus cost basis. Totals are marked incomplete if any holding lacks a price. Amounts exclude fees, taxes, dividends and currency conversion.

## Capstone scope

This version binds to loopback and assumes one trusted local user. Prices are manually recorded. OAuth, multi-user isolation, external market-data refresh, authenticated MCP tools, monthly scheduling, agent evaluation evidence and a hosted deployment are outstanding. Keep the server on loopback.
