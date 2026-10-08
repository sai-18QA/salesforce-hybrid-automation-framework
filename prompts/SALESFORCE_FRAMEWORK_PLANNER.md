# SALESFORCE HYBRID AUTOMATION FRAMEWORK - PLANNER INSTRUCTIONS

## Objective

Design a professional, scalable Salesforce Hybrid Automation Framework using Playwright with TypeScript.

The framework should represent a real-world automation framework suitable for an engineer with 5+ years of automation experience.

Use the existing project as the starting point.

Do NOT generate implementation code yet.

Do NOT modify existing project files yet.

The first objective is to analyze the application, test cases, framework requirements, architecture, and implementation strategy.

The Planner output must be reviewed by a human before Generator is allowed to implement the framework.

---

# 1. Existing Technology Stack

The project uses:

- Playwright Test
- TypeScript
- Node.js
- VS Code
- Git
- GitHub
- Playwright MCP
- GitHub Copilot
- Faker
- MySQL capability for future DB validation
- Playwright APIRequestContext for API automation

The project already contains:

- package.json
- package-lock.json
- playwright.config.ts
- tsconfig.json
- tests/
- .vscode/
- MCP configuration

Analyze the existing configuration before proposing changes.

Do not unnecessarily replace or recreate existing configuration.

---

# 2. Salesforce Application

The application under automation is Salesforce.

The Salesforce URL, username, and password must be obtained from environment variables.

Do NOT hardcode credentials.

Expected environment variables:

SF_BASE_URL
SF_USERNAME
SF_PASSWORD

Real credentials must remain outside source control.

---

# 3. Authentication Strategy

Analyze and design the Salesforce authentication strategy.

Consider:

- Login page
- Username
- Password
- MFA/OTP if applicable
- Authentication reuse
- Storage State
- Initial authentication setup
- Reuse of authenticated sessions

The framework should avoid performing full authentication unnecessarily for every test.

If MFA/OTP is required, design the framework so that authentication can be established once and the authenticated browser state can be reused through Playwright Storage State.

Do NOT put OTP values or secrets in source code or .env.

Explain how authentication should work in:

- Local execution
- CI/Jenkins execution

---

# 4. Business Test Cases

The following test cases must be automated.

## TC001 - Create Task

Steps:

1. Launch Salesforce application.
2. Login with valid credentials.
3. Click App Launcher.
4. Click View All.
5. Search for Task.
6. Select Task.
7. Click New Task from the dropdown.
8. Enter Subject = Email.
9. Select Status = Waiting on someone else.
10. Select Priority = Low.
11. Save.
12. Verify that the task-created confirmation message is displayed.

---

## TC002 - Edit Task

Steps:

1. Launch Salesforce application.
2. Login.
3. Click App Launcher.
4. Click View All.
5. Search/select Task.
6. Locate the Email task.
7. Open the task dropdown.
8. Select Edit.
9. Set Due Date = today's date.
10. Set Priority = High.
11. Set Status = Completed.
12. Save.
13. Verify the updated task fields.

---

## TC003 - Delete Task

Steps:

1. Launch Salesforce application.
2. Login.
3. Click App Launcher.
4. Click View All.
5. Search/select Task.
6. Locate the Email task.
7. Open the task dropdown.
8. Select Delete.
9. Verify that the task has been deleted.

---

# 5. Analyze the Salesforce Application

Before designing Page Objects, analyze the application structure.

Identify:

- Login page
- App Launcher
- View All
- Task application/page
- Task creation screen
- Task edit screen
- Task delete action
- Task list/table
- Confirmation messages
- Dropdown menus
- Forms
- Common Salesforce components
- Reusable navigation flows

Identify which elements are reusable across TC001, TC002, and TC003.

Do not duplicate the same automation logic across tests.

---

# 6. Locator Strategy

Design a professional locator strategy.

Prefer stable locators such as:

- getByRole()
- getByLabel()
- getByText() where appropriate
- data-testid where available
- Salesforce-specific stable attributes where appropriate

Use CSS/XPath only when necessary.

Explain the locator strategy and fallback strategy.

Do not use fragile selectors unnecessarily.

---

# 7. Page Object Model

Design a maintainable POM architecture.

Determine the required Page Objects based on the Salesforce application.

Potential areas include:

- LoginPage
- AppLauncherPage
- TaskPage
- TaskFormPage

Do not create unnecessary Page Objects.

Page Objects should contain:

- Locators
- Page-level actions
- Business-level reusable methods

Tests should not contain raw locator implementation.

Tests should be readable from a business perspective.

---

# 8. Wrapper / Utility Layer

Design a reusable wrapper/helper layer.

Consider common operations such as:

- click
- fill
- selectOption
- getText
- getAttribute
- isVisible
- waitForElement
- navigation
- assertions where appropriate

Determine which methods genuinely belong in a wrapper.

Do not create wrapper methods simply for the sake of abstraction.

Avoid unnecessary abstraction.

---

# 9. Object-Oriented Design

Use OOP concepts where they provide real architectural value.

Evaluate the appropriate use of:

- Classes
- Encapsulation
- Abstraction
- Inheritance
- Interfaces
- Composition
- Access modifiers
- Constructors

Explain WHY each OOP concept is used.

Do not force interfaces, abstract classes, inheritance, or other OOP concepts where they do not provide a real benefit.

Follow SOLID principles where practical.

---

# 10. Custom Fixtures

Design a custom Playwright fixture architecture.

Determine which Page Objects and services should be injected through fixtures.

The test should ideally be able to use business-level objects instead of repeatedly creating Page Object instances.

Explain:

- Fixture structure
- Fixture scope
- Dependency relationships
- Reusability
- Maintainability

---

# 11. Test Data Strategy

Design a test-data strategy.

Use Faker only for data that genuinely needs to be dynamic.

For example:

The requirement:

Subject = Email

is a fixed business requirement and should NOT be randomly generated.

Dynamic data may be used where uniqueness is required.

Explain:

- Static test data
- Dynamic test data
- Faker usage
- Test data separation
- Environment-specific data

---

# 12. API Automation Layer

Design an API layer using Playwright APIRequestContext.

The API layer should support reusable operations such as:

- GET
- POST
- PUT
- PATCH
- DELETE

Design reusable:

- API client
- Request configuration
- Headers
- Authentication
- Payload handling
- Response validation
- Status code validation

Explain where API automation can improve the UI tests.

Possible use cases:

- Test data creation
- Test data cleanup
- Preconditioning
- Backend validation
- Faster setup
- Integration testing

Do not invent Salesforce API credentials or endpoints.

---

# 13. Database Layer

Design a database abstraction layer using mysql2 for future database validation.

Do NOT invent:

- DB host
- DB port
- DB username
- DB password
- DB name
- SQL queries

The framework should provide an architectural extension point for DB testing.

Design:

- DB connection/pool
- Query utility/repository
- Parameterized queries
- Connection management
- Result handling

Tests must not contain raw database connection logic.

---

# 14. Hybrid UI + API + DB Strategy

Design how UI, API, and DB can work together.

For example:

API/DB
   ↓
Prepare data
   ↓
UI
   ↓
Perform business operation
   ↓
UI validation
   ↓
API/DB validation

Explain when each layer should be used.

Do not force every test to use all three layers.

Use the cheapest and most reliable validation layer where appropriate.

---

# 15. Environment Configuration

Design support for multiple environments such as:

- QA
- Staging
- Production

Use environment variables/configuration rather than hardcoded values.

Consider:

- Base URL
- Credentials
- API configuration
- DB configuration
- Environment selection

The same test code should be reusable across environments.

---

# 16. Reporting and Debugging

Design a professional reporting strategy.

Consider:

- Playwright HTML report
- Screenshots
- Traces
- Videos where appropriate
- Console/logging strategy
- Failure diagnostics

Explain when screenshots, traces, and videos should be captured to avoid unnecessary storage consumption.

---

# 17. Tags

Design a tagging strategy such as:

@smoke
@sanity
@regression
@ui
@api
@db
@integration

Explain how tests can be selectively executed.

---

# 18. Parallel Execution and Scalability

The framework must be scalable for a large number of tests.

Design:

- Workers
- Parallel execution
- Browser projects
- Retries
- CI execution
- Test isolation
- Data isolation

Consider how the framework could eventually support thousands of tests.

Avoid designs that create shared-state problems.

---

# 19. Browser Strategy

Analyze the appropriate browser execution strategy.

Consider:

- Chromium
- Firefox
- WebKit

Explain whether all tests should run on all browsers or whether browser coverage should be controlled by execution profile.

---

# 20. Jenkins / CI-CD

Design Jenkins integration.

Consider:

- Environment variables
- Jenkins credentials
- Headless execution
- Parallel execution
- Retry strategy
- Reports
- Artifacts
- Failure diagnostics

Do NOT place credentials directly into Jenkinsfiles or source code.

Explain how local execution and Jenkins execution can use the same framework.

---

# 21. GitHub

Design the repository structure for maintainability.

Consider:

- Source code
- Tests
- Page Objects
- Fixtures
- API
- DB
- Utilities
- Test data
- Configuration
- Authentication
- Reports

Ensure sensitive files remain excluded from Git.

---

# 22. Playwright MCP

Analyze how the existing Playwright MCP configuration can support this project.

Do not unnecessarily install another MCP server.

Explain how MCP can help with:

- Application exploration
- Test planning
- Locator discovery
- Test execution
- Debugging

Clearly distinguish:

MCP = AI interaction/tooling layer

from:

Playwright Framework = actual automation implementation.

---

# 23. Planner / Generator / Healer Workflow

Design the AI-assisted development workflow:

Planner
   ↓
Architecture and test plan
   ↓
Human review
   ↓
Generator
   ↓
Framework implementation
   ↓
Test execution
   ↓
Healer
   ↓
Failure analysis and repair
   ↓
Re-execution

Planner must NOT directly start implementation.

Human approval is required before Generator creates or modifies framework code.

---

# 24. Recommended Folder Structure

Design the final folder structure.

Consider:

tests/
pages/
fixtures/
utils/
api/
db/
data/
config/
auth/
prompts/

But do not blindly create these folders.

Determine which folders are actually required and explain their purpose.

The existing project uses:

tests/

Do not rename it to specs/.

---

# 25. Test Design

Tests should be concise and business-readable.

Avoid:

- Raw locators in tests
- Duplicate login logic
- Duplicate navigation logic
- Direct database connections
- Hardcoded credentials
- Unnecessary waits
- Unnecessary abstraction

Tests should describe business intent.

---

# 26. Code Quality

Design coding standards for:

- Naming conventions
- TypeScript typing
- async/await
- Error handling
- Logging
- Reusability
- Maintainability
- SOLID principles
- DRY principle
- Separation of concerns

Avoid over-engineering.

---

# 27. Required Planner Output

Before generating any code, provide a detailed planning document containing:

1. Existing project analysis
2. Salesforce application analysis
3. Test-case analysis
4. Test strategy
5. Automation architecture
6. Recommended folder structure
7. Page Object design
8. Wrapper/helper design
9. Custom fixture design
10. OOP design and justification
11. API architecture
12. DB architecture
13. Test-data strategy
14. Authentication strategy
15. Storage State strategy
16. Environment configuration
17. Reporting strategy
18. Tagging strategy
19. Browser strategy
20. Parallel execution strategy
21. Jenkins strategy
22. GitHub strategy
23. MCP strategy
24. Planner/Generator/Healer workflow
25. Scalability considerations
26. Risks
27. Assumptions
28. Implementation sequence

For every major architectural decision, explain WHY it is recommended.

---

# 28. Critical Restrictions

DO NOT:

- Generate implementation code yet.
- Modify existing framework files.
- Create Page Objects yet.
- Create fixtures yet.
- Create API classes yet.
- Create DB classes yet.
- Rewrite playwright.config.ts yet.
- Rewrite package.json yet.
- Invent Salesforce API details.
- Invent database details.
- Hardcode credentials.
- Put passwords or secrets into source code.
- Automate OTP blindly.
- Force every OOP concept into the framework.
- Over-engineer the framework.

The Planner's responsibility at this stage is ANALYSIS + DESIGN + PLAN.

Wait for human review and approval before implementation begins.

---

# Final Planner Deliverable

Return a professional architecture and implementation plan suitable for a 5+ years experienced automation engineer.

Clearly separate:

- What already exists
- What should be retained
- What should be changed
- What should be created
- Why each change is required
- Implementation priority
- Dependencies
- Risks
- Open questions

Do not implement anything until the plan has been reviewed and approved.