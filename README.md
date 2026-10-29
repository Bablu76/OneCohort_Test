# OneCohort Test Automation Suite

A Selenium-based automated test suite for the OneCohort web application. This project validates the application's functionality by simulating real user interactions in a browser and checking whether the app behaves correctly.

## 1) Project Overview

This repository is not the application itself. It is the test automation framework that verifies the app works as expected from the user’s point of view.

The project is designed to automate critical workflows such as:
- login and role-based access
- dashboard validation
- navigation and page checking
- create/edit/delete operations
- validation alerts and error handling
- cohort and manager-related flows
- analytics and reporting views
- logout behavior

The framework is built using:
- Java
- Maven
- Selenium WebDriver
- TestNG
- WebDriverManager
- ExtentReports
- Apache POI

## 2) Why This Testing Approach?

This project follows UI automation using Selenium and the Page Object Model (POM).

### Why UI automation?
Because the app is browser-based, the most important validation is whether real users can successfully complete workflows in the browser.

This includes:
- login with valid credentials
- proper redirection after login
- correct navigation between screens
- field validation
- alerts and errors shown to users
- dashboard content verification
- role-specific behavior

### Why Page Object Model (POM)?
The Page Object Model makes the framework easier to maintain and scale.

Instead of writing raw Selenium locators across every test, each screen is represented by a page class, such as:
- LoginPage
- HomePage
- DashboardPage
- CohortManagementPage
- SystemConfigPage
- EmployeePage
- LeavePage
- BatchOwner pages
- Manager pages
- Leader pages
- CR pages

Each page object contains:
- UI locators
- reusable interaction methods
- page-specific validation logic

This results in:
- cleaner test code
- reduced duplication
- easier maintenance when the UI changes
- more readable tests

---

## 3) What Type of Testing Is This?

This project is mainly a functional UI automation test suite.

### Functional Testing
It verifies that the app does what it is supposed to do, such as:
- user can log in
- correct page loads after login
- forms accept valid data
- alerts appear for invalid data
- dashboards show expected elements
- workflows work as expected

### Regression Testing
The suite is also structured to support regression checks, ensuring that existing features still work after new changes.

### Negative Testing
The project checks invalid or incomplete user input, such as:
- empty user ID
- missing service line selection
- missing POC ID
- missing cohort ID
- invalid role-based actions

These tests make sure the application handles bad input correctly and shows meaningful validation messages.

### Role-Based Testing
The app supports multiple roles, so the test suite is designed around real user journeys for:
- Super Admin
- Manager
- Leader
- Batch Owner
- CR
- Employee

This is important because different roles often have different flows and permissions.

---

## 4) Project Structure

```text
OneCohort_Test/
├── README.md
├── pom.xml
├── .gitignore
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/cts/mfrp/onecohort/
│   │           ├── base/
│   │           │   ├── BaseTest.java
│   │           │   └── BaseClassTest.java
│   │           ├── constants/
│   │           │   ├── AppConstants.java
│   │           │   └── AppURLs.java
│   │           ├── pages/
│   │           │   ├── BasePage.java
│   │           │   ├── LoginPage.java
│   │           │   ├── HomePage.java
│   │           │   ├── DashboardPage.java
│   │           │   ├── EmployeePage.java
│   │           │   ├── LeavePage.java
│   │           │   ├── LeftNavPage.java
│   │           │   ├── SuperAdminDashboardPage.java
│   │           │   ├── SystemConfigPage.java
│   │           │   ├── analytics/
│   │           │   ├── batchowners/
│   │           │   ├── cohort/
│   │           │   ├── components/
│   │           │   ├── cr/
│   │           │   ├── leader/
│   │           │   └── managers/
│   │           └── utils/
│   │               ├── ConfigReader.java
│   │               ├── DriverManager.java
│   │               ├── ExcelUtils.java
│   │               ├── ExtentManager.java
│   │               ├── ExtentReportListener.java
│   │               ├── RetryAnalyzer.java
│   │               ├── ScreenshotUtils.java
│   │               └── WaitUtils.java
│   └── test/
│       ├── java/
│       │   └── com/cts/mfrp/onecohort/
│       │       ├── listeners/
│       │       │   └── TestListener.java
│       │       ├── tests/
│       │       │   ├── LoginTest.java
│       │       │   ├── HomePageTest.java
│       │       │   ├── LeftNavPanelTest.java
│       │       │   ├── CohortManagementTest.java
│       │       │   ├── EmployeeTest.java
│       │       │   ├── LeaveTest.java
│       │       │   ├── SystemConfigPageTest.java
│       │       │   ├── SuperAdminDashboardChartsTest.java
│       │       │   ├── SuperAdminLogoutTest.java
│       │       │   ├── analytics/
│       │       │   ├── batchowners/
│       │       │   ├── cohort/
│       │       │   ├── cr/
│       │       │   ├── leader/
│       │       │   └── managers/
│       └── resources/
│           ├── config.properties
│           ├── config-staging.properties
│           ├── suites/
│           │   ├── testng.xml
│           │   ├── smoke-suite.xml
│           │   ├── sanity-suite.xml
│           │   └── parallel-testng.xml
│           └── testdata/
│               ├── BatchOwnerTestData.xlsx
│               ├── CohortTestData.xlsx
│               └── ManagerTestData.xlsx
```

### Why this structure matters

#### base package
Contains browser lifecycle setup and reusable driver configuration.
- opens the browser
- configures waits
- provides access to the driver
- closes the browser after execution

This keeps tests consistent and reduces duplication.

#### pages package
Contains page objects that represent screens in the application.
Each page class knows:
- what elements exist on that page
- how to interact with those elements
- how to validate the page state

This is the core of the Page Object Model.

#### tests package
Contains the actual business test scenarios such as:
- login tests
- dashboard tests
- logout validation
- cohort flows
- manager flows
- negative validation

#### utils package
Contains reusable helper code for:
- reading configuration
- wait handling
- screenshots
- reports
- retries
- Excel data handling

#### resources package
Contains:
- environment config
- TestNG suite XML definitions
- test data files

---

## 5) Where Are the Reports?

The project includes reporting support through ExtentReports.

Key files:
- `src/main/java/com/cts/mfrp/onecohort/utils/ExtentManager.java`
- `src/main/java/com/cts/mfrp/onecohort/utils/ExtentReportListener.java`

These utilities generate HTML reports with:
- pass/fail status
- test descriptions
- execution logs
- screenshots for failed steps

This helps in debugging failures and tracking test health.

---

## 6) Configuration

The main configuration file is:

`src/test/resources/config.properties`

Example:

```properties
base.url=https://one-cohort-1.onrender.com
username=Admin
password=admin123
browser=chrome
headless=false
implicit.wait=10
explicit.wait=15
page.load.timeout=30
```

This file controls:
- the app URL
- browser type
- headless mode
- wait durations
- user IDs and test identifiers

This keeps the framework configurable and reusable across environments.

---

## 7) How to Run This Project

## Prerequisites

Make sure you have:
- Java 21 installed
- Maven installed
- A supported browser installed (Chrome, Firefox, or Edge)
- Network access to the application URL

---

## Run the full test suite

From the project root:

```bash
mvn test
```

This runs the default configured TestNG suite.

---

## Run the smoke suite

```bash
mvn test -DsuiteXmlFile=src/test/resources/suites/smoke-suite.xml
```

The smoke suite is intended for quick validation of the most critical flows.

---

## Run by TestNG group

Examples:

```bash
mvn test -Dgroups=smoke
mvn test -Dgroups=negative
mvn test -Dgroups=dashboard
mvn test -Dgroups=batchowner
mvn test -Dgroups=manager
mvn test -Dgroups=leader
mvn test -Dgroups=cr
```

This helps you run only the tests relevant to a specific area.

---

## Run a specific test class

```bash
mvn -Dtest=LoginTest test
```

---

## Run a specific suite

```bash
mvn test -DsuiteXmlFile=src/test/resources/suites/testng.xml
```

---

## Typical Execution Flow

1. Maven triggers TestNG
2. TestNG reads the suite XML and test classes
3. Browser is initialized from config
4. Test scripts navigate through the app
5. Assertions validate expected behavior
6. Results and screenshots are captured in reports

---

## 8) Why This Project Is Valuable

This project helps validate the real user journey in the application and ensures that critical business functionality works as expected.

It is useful because it:
- checks real browser behavior
- verifies role-based access
- catches regressions early
- reduces manual testing effort
- helps validate release readiness

For a multi-role business portal like OneCohort, this is a very practical and scalable testing strategy.

---

## 9) Summary

This repository is a Selenium-based UI automation framework built to validate the OneCohort application across key business workflows.

It combines:
- Selenium for browser automation
- TestNG for test execution
- Maven for project setup and execution
- Page Object Model for structure and maintenance
- ExtentReports for reporting and debugging

The design makes the project readable, scalable, and maintainable for ongoing regression and functional testing.

---

## 10) Contributing and Permission to Edit

This project is intended for learning, testing, and improvement. If you would like to contribute or make changes to this repository, please ask for permission from the repository owner before editing or submitting modifications.

Contributors should:
- clearly state the purpose of the change
- avoid making unauthorized edits
- keep the project structure and testing style consistent
- communicate before large changes or refactors

If you want to update, improve, or extend this project, please contact the repository owner first and obtain permission before making edits.

---

## Repository

`Bablu76/OneCohort_Test`

This project is intended to automate and validate real user journeys in the OneCohort application across multiple roles and workflows.
