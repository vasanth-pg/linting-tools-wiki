Frontend Linting Guide

## Table of Contents

- [Introduction](#1-introduction)
- [What is Linting?](#2-what-is-linting)
- [ESLint](#3-eslint)
- [Prettier](#4-prettier)
- [ESLint vs Prettier](#5-eslint-vs-prettier)
- [Installation](#6-installation)
- [Configuration](#7-configuration)
- [Running Linting](#8-running-linting)
- [Best Practices](#9-best-practices)
- [Troubleshooting](#10-troubleshooting)

# 1. Introduction
	Modern software development involves multiple developers working on the same codebase. Without a common coding standard, the project can become difficult to read, review and maintain. Frontend linting helps enforce consistent coding practices and identifies potential issues before the code is merged.
	This project uses ESLint for code quality checks and prettier for automatic code formatting. Together, they help maintain a clean, consistent and maintainable codebase.

# 2. What is Linting?
	Linting is the process of analyzing source code to identify coding issues, enforce coding standards and improve code quality without executing the program.
	think of linting as a grammar checker for code. Just as a grammer checker highlights spelling and grammatical mistakes before publishing a document, a linter highlights potential coding coding issues before the ocde is reviewed or deployed.

## Benefits
- Detects common coding mistakes early
- Enforce consistent coding standards
- Improves code readability
- Reduces code review effort
- Encourages best practices
- Makes long-term maintenance easier

# 3. ESLint

## What is ESLint?
	ESLint is an open source linting tool for javascript. It analyzes source code based on configurable rules and reports issues related to code quality, coding standards, and best practices.

## How ESLint works?
	When ESLint is executed:
1. Reads the source code
2. Analyzes the code structure
3. Compares the code against configured rules
4. Reports violations as warnings or errors
5. Automatically fixes supported issues when using the `--fix` option

## Common issues detected
- Unused variables
- Undefined variables
- Use of `var` instead of `let` or `const`
- Missing semicolons
- Incorrect quotation marks
- Inconsistent indentation
- Unnecessary whitespace

## Example:
	During a code review, a developer accidentally references an undefined variable. ESLint detects the issue before the pull request is merged, preventing a potential runtime error.


# 4. Prettier

## what is prettier?
	Prettier is an opinionated code formatter that automatically formats source code into a consistent style.
	Unlike ESLint, Prettier focuses only on formatting. it does not detect code quality issues or programming mistakes.

## What Prettier formats?
- Indentation
- Spacing
- Semicolons
- Quotes
- Line wrapping
- Blank lines
- Object and array formatting

## why use prettier?
	Using a consistent formatting style:
- improves readability
- eliminates formatting discussions during code review
- keeps the entire codebase visually consistent
- saves developer time by formatting automatically

## Example:
	Different developers may format code differently. Prettier automatically applies a consistent formatting style, ensuring the entire codebase looks uniform without manual effort.


# 5. ESLint vs Prettier

| Feature | ESLint | Prettier |
|---------|---------|----------|
| Primary Purpose | Checks code quality | Formats code |
| Detects Bugs | ✔ Yes | ✘ No |
| Enforces Coding Standards | ✔ Yes | ✘ No |
| Enforces Formatting Style | Limited | ✔ Yes |
| Reports Warnings and Errors | ✔ Yes | ✘ No |
| Automatically Fixes Issues | ✔ Supported for some issues | ✔ Formats nearly all style-related issues |

## Why Use Both?
ESLint and prettier solve different problems
- ESLint focuses on code quality and coding standards
- Prettier focuses on consistent formatting
Using both provides a cleaner development workflow and reduces unnecessary code review comments.

Now that we understand the purpose of ESLint and Prettier, the next step is to install and configure them for the project.

# 6. Installation
## Prerequisites
Before installing ESLint and Prettier, ensure the following are installed on your system:
- Node.js
- npm (comes bundled with Node.js)
Verify the installation by running:
```
node -v
npm -v
```
If version numbers are displayed, your environment is ready.
---
Install ESLint
Install ESLint as a development dependency:
```
npm install -D eslint
```
---
Install Prettier
Install Prettier as a development dependency:
```
npm install -D prettier
```
---
Install ESLint-Prettier Integration
Install the integration package to prevent conflicts between ESLint and Prettier formatting rules:
```
npm install -D eslint-config-prettier
```
## Why?
```
eslint-config-prettier disables ESLint formatting rules that might conflict with Prettier, allowing both tools to work together smoothly.
```
# 7. Configuration
After installing ESLint and Prettier, they need to be configured according to the project's coding standards. This section explains how to initialize ESLint, configure rules, use predefined rule sets, configure Prettier, and simplify common tasks using npm scripts.
---
## 7.1 Initialize ESLint
Initialize ESLint by running:
```
npx eslint --init
```
The setup wizard will ask a series of questions about your project, including:
- The type of files you want to lint
- The module system (ES Modules or CommonJS)
- The framework being used (React, Vue, None, etc.)
- The environment (Browser, Node.js, etc.)
Once completed, ESLint generates a configuration file (for example, eslint.config.mjs) in the project root.
---
## 7.2 Understanding the ESLint Configuration File
The ESLint configuration file defines how ESLint analyzes your source code.
## Example:
```
export default [
  {
    rules: {
      "no-console": "warn",
      "no-unused-vars": "error",
      "prefer-const": "error"
    }
  }
];
```
The rules section tells ESLint which coding standards to enforce.
## Rule Severity
Every ESLint rule has a severity level.
| Severity | Description |
|----------|-------------|
| off | Disables the rule |
| warn | Reports a warning but does not fail linting |
| error | Reports an error and may fail the linting process |
## Example:
```
rules: {
  "no-console": "warn",
  "no-unused-vars": "error",
  "prefer-const": "error"
}
```
---
## 7.3 Adding Custom Rules
Projects can define their own coding standards by adding custom rules.
## Example:
```
rules: {
  "no-console": "warn",
  "prefer-const": "error",
  "semi": ["error", "always"],
  "quotes": ["error", "double"]
}
```
## Common ESLint Rules
| Rule | Description |
|------|-------------|
| `no-console` | Warns when `console.log()` is used |
| `no-unused-vars` | Detects variables that are declared but never used |
| `prefer-const` | Suggests using `const` instead of `let` when a variable is not reassigned |
| `semi` | Enforces semicolon usage |
| `quotes` | Enforces single or double quotation marks |
---
## 7.4 Using Shareable Configurations
Instead of defining every rule manually, ESLint allows you to reuse predefined rule sets maintained by the community. These are called Shareable Configurations.
A shareable configuration is simply a collection of ESLint rules that can be shared across multiple projects.
Some popular shareable configurations are:
- ESLint Recommended
- Airbnb
- Google
- Standard
Using a shareable configuration helps teams quickly adopt consistent coding standards without manually configuring hundreds of rules.
---
Example: ESLint Recommended
```
extends: [
  "js/recommended"
]
```
This enables ESLint's recommended set of rules.
---
Example: Airbnb Configuration
Install Airbnb's configuration package.
```
npm install -D eslint-config-airbnb eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y
```
Then extend it in your ESLint configuration.
```
extends: [
  "airbnb"
]
```
Airbnb provides a comprehensive set of JavaScript and React coding standards maintained by the Airbnb engineering team.
---
How Do I Know Which Rules a Shareable Configuration Uses?
When using a shareable configuration like Airbnb, a common question is:
```
"How do I know which rules it already contains?"
```
You don't need to memorize the rules. There are several ways to find them.
Option 1 – Official Documentation (Recommended)
Most shareable configurations provide official documentation describing the rules they include and any customizations they make.
This is the recommended approach when learning a new configuration.
---
Option 2 – Inspect the Configuration Files
After installation, the configuration package is available inside the node_modules directory.
## Example:
node_modules/
```
└── eslint-config-airbnb/
    ├── index.js
    ├── base.js
    └── rules/
```
The rules folder contains the rule definitions used by that configuration. You can inspect these files to understand which rules are enabled or customized.
---
Option 3 – Print the Final ESLint Configuration (Recommended for Debugging)
ESLint can display the complete configuration being applied to a file.
```
npx eslint --print-config src/index.js
```
This command combines:
- Shareable configurations
- Plugins
- Your custom rules
and prints the final configuration.
For example, searching the output for no-console shows the final rule currently being applied.
This is one of the most useful commands when troubleshooting or understanding ESLint behavior.
---
## 7.5 Overriding Rules
Even when using a shareable configuration, you can customize individual rules to meet your project's requirements.
## Example:
```
export default [
  {
    extends: ["airbnb"],
```

```
    rules: {
      "no-console": "warn"
    }
  }
];
```
In this example:
- Airbnb provides the default coding standards.
- The project overrides the no-console rule and changes it to a warning.
Project-specific rules always take precedence over rules defined in a shareable configuration.
---
## 7.6 Plugins
Plugins extend ESLint by adding rules for specific languages, frameworks, or libraries.
## Common plugins include:
| Plugin | Purpose |
|--------|---------|
| `eslint-plugin-react` | Adds React-specific linting rules |
| `eslint-plugin-react-hooks` | Validates proper use of React Hooks |
| `eslint-plugin-import` | Checks import and export statements |
| `eslint-plugin-jsx-a11y` | Improves accessibility in JSX |
Example installation:
```
npm install -D eslint-plugin-react
```
Plugins are then added to the ESLint configuration file to enable their rules.
---
## 7.7 Configure Prettier
Create a .prettierrc file in the project root.
## Example:
```
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "printWidth": 100
}
```
## Common Prettier Options
| Option | Description |
|--------|-------------|
| `semi` | Adds semicolons at the end of statements |
| `singleQuote` | Uses single quotes instead of double quotes |
| `tabWidth` | Sets the number of spaces per indentation level |
| `printWidth` | Wraps lines longer than the specified width |
---
## 7.8 Prevent ESLint and Prettier Conflicts
ESLint and Prettier may sometimes apply different formatting rules.
To prevent conflicts, install:
```
npm install -D eslint-config-prettier
```
Then include it in the ESLint configuration.
```
extends: [
  "js/recommended",
  "prettier"
]
eslint-config-prettier disables ESLint formatting rules that overlap with Prettier, allowing both tools to work together without conflicts.
```
---
## 7.9 Adding npm Scripts
To simplify running ESLint and Prettier, add the following scripts to the scripts section of package.json.
```
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier . --write"
  }
}
```
You can now use the following commands:
| Command | Description |
|---------|-------------|
| `npm run lint` | Checks the project for linting issues |
| `npm run lint:fix` | Automatically fixes supported ESLint issues |
| `npm run format` | Formats the project using Prettier |

# 8. Running Linting
Once ESLint and Prettier have been installed and configured, they can be used to analyze and format the project's source code.
---
## Check for Linting Issues
Run the following command to analyze the project for linting issues:
```
npm run lint
```
This command scans the project and reports any warnings or errors based on the configured ESLint rules.
Example output:
```
src/app.js
```
  12:5   warning  Unexpected console statement        no-console
  25:10  error    'username' is not defined           no-undef

✖ 2 problems (1 error, 1 warning)
---
## Automatically Fix Supported Issues
Run:
```
npm run lint:fix
```
This command automatically fixes issues that ESLint can safely correct, such as:
- Missing semicolons
- Incorrect quotation marks
- Indentation
- Extra whitespace
Some issues, such as unused variables or undefined variables, require manual intervention and will not be fixed automatically.
---
## Format the Project
Run:
```
npm run format
```
This command formats the project using Prettier according to the settings defined in .prettierrc.
---
## Recommended Development Workflow
A typical development workflow is:
1. Write code.
2. Format the code using Prettier.
3. Run ESLint to detect coding issues.
4. Fix any reported warnings or errors.
5. Commit the changes.
6. Create a Pull Request.
Following this workflow helps reduce code review comments and ensures the codebase remains consistent.
---
# 9. Best Practices
Following these best practices helps maintain a consistent and high-quality codebase.
- Run npm run lint before creating a Pull Request.
- Run npm run format before committing code.
- Fix linting errors instead of disabling rules whenever possible.
- Keep ESLint and Prettier configuration consistent across the project.
- Use shareable configurations (such as Airbnb or ESLint Recommended) to maintain coding standards.
- Install the ESLint and Prettier VS Code extensions for real-time feedback.
- Review new ESLint rules before enabling them for the entire project.
- Avoid unnecessary custom rules unless required by the project.
---
# 10. Troubleshooting
ESLint Command Not Found
## Problem
```
'eslint' is not recognized as an internal or external command.
```
## Solution
Ensure ESLint is installed.
```
npm install -D eslint
```
---
Prettier Is Not Formatting Code
## Possible Causes
- Prettier is not installed.
- The .prettierrc file is missing.
- The VS Code Prettier extension is not installed or enabled.
---
ESLint and Prettier Reporting Different Formatting
Cause
Both tools may be applying formatting rules.
## Solution
```
Install and configure eslint-config-prettier.
npm install -D eslint-config-prettier
```
---
Rules Are Not Being Applied
## Possible Causes
- Incorrect ESLint configuration.
- Wrong configuration file.
- ESLint is not reading the expected configuration.
## Solution
Print the active configuration:
```
npx eslint --print-config src/index.js
```
Verify that the expected rules are present.
---
```
npm Scripts Are Not Working
```
Verify that the scripts exist in package.json.
## Example:
```
{
  "scripts": {
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier . --write"
  }
}
```
