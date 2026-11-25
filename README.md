# Assignment: Stock Portfolio Performance Report

## 1. Overview

In this assignment, you will build a Python application that generates a stock portfolio performance report using current market data obtained from a public API.

This project combines several skills developed throughout the course, including:

- Reading and writing CSV files
- Making HTTP requests
- Working with external APIs
- Unit testing with pytest
- Mocking HTTP requests
- Packaging Python applications
- GitHub Actions automation
- Test-Driven Development (TDD)

---

## 2. Learning Outcomes

By completing this assignment, you will demonstrate your ability to:

- Read data from CSV files.
- Write data to CSV files.
- Consume REST APIs using Python.
- Test file operations.
- Test external API calls using mocks.
- Create a reusable and modular Python application.
- Package and distribute a Python project.
- Use GitHub Actions for automated testing.

---

## 3. Scenario

You have been asked to develop a command-line application that generates up-to-date performance reports for an investment portfolio.

The application will:

1. Read stock holdings from an input CSV file.
2. Retrieve current stock prices from an online API.
3. Calculate portfolio performance metrics.
4. Generate an output CSV report.
5. Be installable and executable from the command line.

---

## 4. Market Data Provider

This assignment will use the **Alpha Vantage API**.

**API Documentation:**

https://www.alphavantage.co/documentation/

**Free API Key Registration:**

https://www.alphavantage.co/support/#api-key

> **Important:** Keep your API key private. Do not commit it to GitHub. Use an environment variable or another secure method to manage your API key.

---

## 5. Command-Line Usage

Your application must be executable from the command line after installation.

**Example:**

```bash
portfolio_report --source portfolio.csv --target report.csv
```

The application should:

- Accept an input CSV file using `--source`.
- Accept an output CSV file using `--target`.
- Process the portfolio holdings.
- Generate the performance report.

---

## 6. Input File Format

The input CSV file contains information about stock holdings.

### Required Columns

| Column | Description |
|---|---|
| `symbol` | Stock ticker symbol |
| `units` | Number of shares owned |
| `cost` | Original purchase price per share |

**Example: `portfolio.csv`**

```csv
symbol,units,cost
AAPL,10,180.00
MSFT,5,350.00
GOOGL,8,140.00
```

---

## 7. Retrieving Market Data

Use the Alpha Vantage API to retrieve the latest stock price.

### Example API Request

```text
https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol=AAPL&apikey=YOUR_API_KEY
```

### Example API Response

```json
{
    "Global Quote": {
        "01. symbol": "AAPL",
        "05. price": "204.29"
    }
}
```

Your application should extract the latest stock price from the API response.

---

## 8. Required Calculations

For each stock holding, calculate the following values:

### 8.1 Book Value

The original value of the stock investment.

```python
book_value = units * cost
```

### 8.2 Market Value

The current value of the stock investment.

```python
market_value = units * latest_price
```

### 8.3 Gain / Loss

The difference between the current market value and the original book value.

```python
gain_loss = market_value - book_value
```

### 8.4 Percentage Change

The percentage gain or loss compared to the original investment.

```python
change = gain_loss / book_value
```

---

## 9. Output CSV Format

Your application must generate a CSV report containing the following columns:

| Column | Description |
|---|---|
| `symbol` | Stock ticker symbol |
| `units` | Number of shares owned |
| `cost` | Original purchase price per share |
| `latest_price` | Latest stock price retrieved from the API |
| `book_value` | Original investment value |
| `market_value` | Current investment value |
| `gain_loss` | Difference between market value and book value |
| `change` | Percentage gain or loss |

**Example output: `report.csv`**

```csv
symbol,units,cost,latest_price,book_value,market_value,gain_loss,change
AAPL,10,180.00,204.29,1800.00,2042.90,242.90,0.1349
```

---

## 10. Handling Invalid Stock Symbols

If a stock symbol cannot be found or the API does not return valid stock price information, your application must:

- Display a warning to the user.
- Skip the invalid symbol.
- Continue processing the remaining records.
- Not terminate the application because of one invalid symbol.

---

## 11. Development Requirements

Develop the application using a **modular design**.

Your application should separate responsibilities into appropriate modules and functions.

### Suggested Functional Components

#### 11.1 CSV Reader
- Read portfolio holdings from an input CSV file.
- Extract the required columns.

#### 11.2 Market Data Service
- Retrieve stock prices from Alpha Vantage.
- Handle API responses and errors.

#### 11.3 Calculation Module

Calculate:

- Book Value
- Market Value
- Gain/Loss
- Percentage Change

#### 11.4 Report Generator
- Convert portfolio holdings into report rows.
- Organize the calculated results.

#### 11.5 CSV Writer
- Write report data to the output CSV file.

#### 11.6 Command-Line Interface
- Process `--source` and `--target` arguments.
- Execute the application.

---

# 12. Testing Requirements

Use **pytest** for all tests.

Your tests must cover file operations, calculations, API requests, and application functionality.

### 12.1 Testing File Operations

Use the built-in pytest fixture:

```python
tmp_path
```

This fixture allows you to create temporary files and directories for testing without modifying actual project files.

### 12.2 Testing HTTP Requests

Install the following package:

```bash
pip install requests-mock
```

**Documentation:**

https://requests-mock.readthedocs.io/en/latest/pytest.html

Mock all API requests in your tests.

**Correct approach:**

```python
requests_mock.get(...)
```

**Incorrect approach during testing:**

```python
requests.get(...)
```

> **Important:** Your tests must never depend on a live API or require an actual internet connection.

---

# 13. Packaging Requirements

Your project must include:

```text
setup.py
```

The package must:

- Install successfully using `pip`.
- Include all required dependencies.
- Create a command-line executable named `portfolio_report`.

### Installation

```bash
pip install .
```

### Execute the Application

```bash
portfolio_report --source portfolio.csv --target report.csv
```

---

# 14. Required Project Structure

Your repository should contain files similar to the following:

```text
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
```

You may organize your project differently, provided your solution remains modular and maintainable.

---

# 15. Test-Driven Development (TDD)

This assignment **must be developed using a Test-Driven Development (TDD) approach**.

For each feature, follow these steps:

1. Write a failing test.
2. Commit the failing test to GitHub.
3. Write the code to make the test pass.
4. Commit the passing implementation.
5. Repeat the process for the next feature.

### Example TDD Commit Messages

| Step | Commit Message |
|---|---|
| 1 | Add CSV reader test |
| 2 | Implement CSV reader |
| 3 | Add stock price request test |
| 4 | Implement stock price retrieval |
| 5 | Add portfolio calculation test |
| 6 | Implement portfolio calculations |

> **Important:** Your GitHub commit history must demonstrate your TDD process. Submitting only the final code without evidence of incremental development will affect your marks.

---

# 16. GitHub Actions

You must configure **GitHub Actions** to automatically run your tests.

### Requirements

- Include the GitHub Actions workflow file in your repository.
- Configure the workflow to execute your pytest test suite.
- Ensure the workflow runs successfully.
- The final workflow run must pass.

Your workflow file should be located at:

```text
.github/workflows/python-tests.yml
```

---

# 17. Evaluation Rubric (25 Marks)

| Evaluation Criteria | Marks |
|---|---:|
| CSV File Reading | 3 |
| API Integration | 4 |
| Portfolio Calculations | 4 |
| CSV Report Generation | 3 |
| Unit Testing (including mocks) | 4 |
| Packaging using `setup.py` | 2 |
| TDD Commit History | 3 |
| GitHub Actions | 2 |
| **Total** | **25** |

---

# 18. Code Style

Follow **PEP 8 Python coding standards** throughout your project.

Your code should demonstrate:

- Consistent indentation.
- Meaningful variable and function names.
- Appropriate comments and documentation.
- Proper organization of modules and functions.
- Readable and maintainable code.

**Penalty:** -1% for each code style violation identified during grading.

---

# 19. Submission Instructions

Before submitting your assignment, ensure that you have completed the following:

1. Push your completed project to GitHub.
2. Verify that all required files are included in your repository.
3. Run your tests using pytest.
4. Verify that GitHub Actions is passing.
5. Ensure your GitHub commit history demonstrates the TDD process.
6. Submit your GitHub repository URL through D2L before the assignment deadline.

---

# 20. Important Notes

- Your solution must work for **any valid portfolio CSV file**, not only the examples shown in this assignment.
- Do not hard-code stock symbols, stock prices, or portfolio values.
- All API requests must be mocked during testing.
- Keep your API key private. Never upload it to GitHub.
- Follow the TDD process throughout development.
- Ensure your application handles invalid stock symbols without terminating the entire process.

**Hard-coded solutions will not receive credit.**

---

## Good Luck!

Remember to follow the Test-Driven Development (TDD) process throughout your development. Commit your work regularly and ensure your application is properly tested before submission.

**Course Grading Policy:** Please refer to the *Evaluation Plan & Grading Policy* available in D2L.
