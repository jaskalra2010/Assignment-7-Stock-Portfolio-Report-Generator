Assignment 7 - Stock Portfolio Report Generator
Overview
In this assignment, you will build a Python application that generates a stock portfolio performance report using current market data obtained from a public API.

This project combines several skills developed throughout the course, including:

Reading and writing CSV files
Making HTTP requests
Working with external APIs
Unit testing with pytest
Mocking HTTP requests
Packaging Python applications
GitHub Actions automation
Test-Driven Development (TDD)
Learning Outcomes
By completing this assignment, you will demonstrate your ability to:

Read data from CSV files
Write data to CSV files
Consume REST APIs using Python
Test file operations
Test external API calls using mocks
Create a reusable and modular Python application
Package and distribute a Python project
Use GitHub Actions for automated testing
Scenario
You have been asked to develop a command-line application that generates up-to-date performance reports for an investment portfolio.

The application will:

Read stock holdings from an input CSV file.
Retrieve current stock prices from an online API.
Calculate portfolio performance metrics.
Generate an output CSV report.
Be installable and executable from the command line.
Market Data Provider
This assignment will use the Alpha Vantage API.

Documentation
https://www.alphavantage.co/documentation/

Free API Key Registration
https://www.alphavantage.co/support/#api-key

Important: Keep your API key private. Do not commit it to GitHub.

Command Line Usage
Your application must be executable from the command line after installation.

Example
portfolio_report --source portfolio.csv --target report.csv
Input File Format
The input CSV file contains information about stock holdings.

Required Columns
Column	Description
symbol	Stock ticker symbol
units	Number of shares owned
cost	Original purchase price per share
Example Input
symbol,units,cost
AAPL,1000,123.56
AMZN,20,2001.10
Retrieving Market Data
Use the Alpha Vantage API to retrieve the latest stock price.

Example Request
https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=AAPL&apikey=YOUR_API_KEY
Example Response
{
    "Global Quote": {
        "01. symbol": "AAPL",
        "05. price": "204.29"
    }
}
