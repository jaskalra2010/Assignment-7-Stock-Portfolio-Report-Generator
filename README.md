# Assignment 7-Stock Portfolio Report Generator

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
Required Calculations
For each stock holding calculate:

Book Value
book_value = units * cost
Market Value
market_value = units * latest_price
Gain / Loss
gain_loss = market_value - book_value
Percentage Change
change = gain_loss / book_value
Output CSV Format
Create a CSV report containing:

Column
symbol
units
cost
latest_price
book_value
market_value
gain_loss
change
Example Output
symbol,units,cost,latest_price,book_value,market_value,gain_loss,change
AAPL,1000,123.56,156.23,123560,156230,32670,0.264
AMZN,20,2001.10,1478.19,40022,29563,-10459,-0.261
Handling Invalid Symbols
If a stock symbol cannot be found:

Display a warning to the user.
Skip the invalid symbol.
Continue processing the remaining records.
Do not terminate the application.
Development Requirements
Develop the application using a modular design.

Suggested Functional Components
CSV Reader
Read the portfolio holdings from a CSV file.

Market Data Service
Retrieve stock prices from Alpha Vantage.

Calculation Module
Calculate:

Book Value
Market Value
Gain/Loss
Percentage Change
Report Generator
Convert holdings into CSV report rows.

CSV Writer
Write report data to the output file.

Command Line Interface
Process --source and --target arguments.

Testing Requirements
Use pytest for all tests.

Testing File Operations
Use the built-in pytest fixture:

tmp_path
Testing HTTP Requests
Install:

pip install requests-mock
Documentation:

https://requests-mock.readthedocs.io/en/latest/pytest.html

Mock all API requests in your tests.

✅ Correct:

requests_mock.get(...)
❌ Incorrect:

requests.get(...)
during testing.

Your tests should never depend on a live API.

Packaging Requirements
Your project must include:

setup.py
The package must:

Install successfully using pip
Include required dependencies
Create a command-line executable named:
portfolio_report
Example
pip install .

portfolio_report --source portfolio.csv --target report.csv
Required Files
Your repository should contain files similar to:

portfolio_report/
│
├── portfolio.py
├── report.py
├── setup.py
├── requirements.txt
├── README.md
│
├── tests/
│   ├── test_portfolio.py
│   └── test_report.py
│
└── .github/
    └── workflows/
        └── python-tests.yml
You may organize the project differently if your solution remains modular and maintainable.

Test-Driven Development (TDD)
This assignment must be developed using a TDD approach.

For each feature:

Write a failing test.
Commit the failing test.
Write the code to make the test pass.
Commit the passing implementation.
Repeat for the next feature.
Example Commit Messages
Step 1: Add CSV reader test
Step 1: Implement CSV reader

Step 2: Add stock price request test
Step 2: Implement stock price retrieval

Step 3: Add portfolio calculation test
Step 3: Implement calculations
GitHub Actions
You must configure GitHub Actions to automatically run your tests.

Requirements
Workflow file submitted
Workflow executes successfully
Final workflow run passes
Evaluation Rubric (25 Marks)
Criteria	Marks
CSV File Reading	3
API Integration	4
Portfolio Calculations	4
CSV Report Generation	3
Unit Testing (including mocks)	4
Packaging (setup.py)	2
TDD Commit History	3
GitHub Actions	2
Total	25
Code Style
Follow PEP 8 coding standards.

Penalty: -1% for each code style violation identified during grading.

Submission Instructions
Push your completed project to GitHub.
Verify that GitHub Actions is passing.
Submit your GitHub repository URL through D2L before the deadline.
Important Note
Your solution must work for any valid portfolio file, not only the examples shown in this assignment.

Hard-coded solutions will not receive credit.

Good luck, and remember to follow the TDD process throughout your development!

The course grading policy is available here:

Evaluation Plan & Grading Policy
