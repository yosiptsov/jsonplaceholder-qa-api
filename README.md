# Postman Tests

A comprehensive API testing suite using Postman collections and Newman CLI. This project contains automated tests for RESTful APIs including JSONPlaceholder and QA Dojo APIs.

## Overview

This repository provides a structured approach to API testing using Postman collections. Tests are executed via Newman, which allows for automated testing in CI/CD pipelines and local environments.

## Prerequisites

- **Node.js** (v14 or higher)
- **npm** (v6 or higher)

## Installation

1. Clone the repository:

```bash
git clone <repository-url>
cd postman-tests
```

2. Install dependencies:

```bash
npm install
```

This installs Newman, the command-line collection runner for Postman.

## Project Structure

```
postman-tests/
├── tests/
│   ├── jsonPlaceholder.postman.json          # JSONPlaceholder API test collection
│   └── qa-dojo-postman-test.postman_collection.json  # QA Dojo API test collection
├── package.json                              # Project dependencies
├── package-lock.json                         # Locked dependency versions
└── README.md                                 # This file
```

## Usage

### Running Tests with Newman

#### JSONPlaceholder API Tests

```bash
npx newman run tests/jsonPlaceholder.postman.json
```

#### QA Dojo API Tests

```bash
npx newman run tests/qa-dojo-postman-test.postman_collection.json
```

### Newman Options

For more advanced options, you can use Newman's command-line flags:

```bash
# Run with specific environment variables
npx newman run tests/jsonPlaceholder.postman.json -e environment.json

# Export test results to HTML
npx newman run tests/jsonPlaceholder.postman.json -r html --reporter-html-export report.html

# Run with custom reporters (cli, json, html)
npx newman run tests/jsonPlaceholder.postman.json -r cli,json --reporter-json-export results.json

# Run with specific iterations
npx newman run tests/jsonPlaceholder.postman.json -n 5
```

## Test Collections

### JSONPlaceholder Tests

Tests for the free JSONPlaceholder API, covering:

- GET requests for individual resources
- Listing resources
- Status code validation
- Response structure verification

**API URL:** https://jsonplaceholder.typicode.com

### QA Dojo Tests

Test suite for QA Dojo API endpoints with various test scenarios and validations.

## Adding New Tests

1. Create or edit a Postman collection in the Postman GUI
2. Export the collection as JSON
3. Place it in the `tests/` directory
4. Run with Newman as shown above

## Environment Configuration

If you need to use environment variables in your tests, create an `environment.json` file in the root directory and reference it when running tests:

```bash
npx newman run tests/jsonPlaceholder.postman.json -e environment.json
```

Example `environment.json`:

```json
{
  "id": "environment-id",
  "name": "Development",
  "values": [
    {
      "key": "baseUrl",
      "value": "https://jsonplaceholder.typicode.com",
      "enabled": true
    }
  ]
}
```

## Continuous Integration

To integrate these tests into your CI/CD pipeline, add the following to your workflow configuration:

```yaml
- name: Run API Tests
  run: npm install && npx newman run tests/jsonPlaceholder.postman.json
```

## Dependencies

- **newman** (^6.2.2) - Command-line collection runner for Postman

## Author

Yurii Osiptsov

## License

ISC

## Additional Resources

- [Newman Documentation](https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/)
- [Postman Collections](https://learning.postman.com/docs/collections/collections-overview/)
- [JSONPlaceholder API](https://jsonplaceholder.typicode.com/)

## Contributing

To add new tests or improve existing ones:

1. Create or modify a Postman collection
2. Export it to the `tests/` directory
3. Run the tests locally to verify they work
4. Submit your changes for review
