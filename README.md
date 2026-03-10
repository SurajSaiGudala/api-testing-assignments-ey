# API Test Template — Data Driven Testing Using Postman

This repository contains a Postman collection template for API testing with test scripts and a data-driven CSV file for running multiple test scenarios.

## Files

- **postman-collection-template.json** — Postman collection (v2.1.0) with pre-built test scripts for REST API operations:
  - `Create Post (example)` — POST request with comprehensive assertions and stores `createdId` in environment for later use
  - `Get Created Post` — GET request using `{{createdId}}` variable with assertions handling both persistent and non-persistent APIs
  - `Get Posts` — List request with schema validation, type checking, and header assertions

- **postman-environment.json** — Environment configuration file for Postman with variables:
  - `baseUrl` — Set to `https://jsonplaceholder.typicode.com` (customizable for your API)
  - `maxResponseTime` — Response time threshold (default: 2000ms) for latency assertions

- **data.csv** — Sample test data for data-driven testing containing:
  - Column headers: `title`, `body`, `userId`
  - 10 test scenarios including quick tests, edge cases, performance tests, and regression tests

- **prompt.txt** — Original prompt used to generate the test scripts

## Quick Start

1. **Open Postman** and import the collection:
   - Import > File > Select `postman-collection-template.json`

2. **Configure the API endpoint:**
   - Edit the `baseUrl` collection variable to point to your API (default: JSONPlaceholder)

3. **Run the tests:**
   - Execute individual requests to test specific endpoints
   - Use **Collection Runner** to run all requests in sequence
   - Use **Data Driven Testing** by uploading `data.csv` for parameterized test runs

## Test Assertions

The collection includes:
- Status code validation (201 for POST, 200 for GET)
- Response content-type verification (application/json)
- Response payload schema validation (presence of required fields)
- Data type validation (string, number types for each field)
- Response time performance checks using `maxResponseTime` variable
- Environment variable storage for request chaining

## Running with Newman (CLI)

To run the collection without the Postman UI using Newman:

```bash
npx newman run postman-collection-template.json --environment postman-environment.json
```

### Using insecure mode (for development only):
```bash
npx newman run postman-collection-template.json --environment postman-environment.json --insecure
```
> ⚠️ Use `--insecure` only for debugging with self-signed certificates. Prefer setting `NODE_EXTRA_CA_CERTS` for production.

## Configuration

### maxResponseTime Variable
- **Purpose:** Sets the acceptable response time threshold (in milliseconds) for assertions
- **Default:** 2000ms
- **How to change:**
  - In Postman: Open collection > Edit `maxResponseTime` variable
  - For Newman: Edit `postman-environment.json` before running, or use environment variable override

### baseUrl Variable
- **Purpose:** API endpoint base URL
- **Default:** `https://jsonplaceholder.typicode.com`
- **How to change:**
  - In Postman: Open collection > Edit `baseUrl` variable
  - For Newman: Edit `postman-environment.json` before running

## Data-Driven Testing

The `data.csv` file contains test scenarios that can be used with Postman's Collection Runner for data-driven testing:

```csv
title,body,userId
"Quick test A","This is a random body A.",1
"Quick test B","This is a random body B.",2
"Lorem ipsum","Lorem ipsum dolor sit amet.",3
"Sample title 4","Sample body content 4.",1
"Edge case title","Edge case body with symbols !@#$%.",4
"Performance test","Large body placeholder text for perf.",2
"Smoke test","Smoke test body.",5
"Regression 1","Regression test body.",3
"Create item X","Create item X body.",2
"Final test","Final test body entry.",1
```

To use this data in Collection Runner:
1. Click **Run** in Postman
2. Select the collection
3. Under **Data**, upload `data.csv`
4. Run the collection — variables will be populated for each test iteration

## Notes

- This template uses Postman's native test assertion library (`pm.test`, `pm.response`, `pm.expect`)
- Customize request bodies, headers, URLs, and assertions as needed for your API
- The "Get Created Post" request includes conditional logic to handle both persistent and mock APIs
- For non-persistent APIs (like JSONPlaceholder), a 404 response is expected and marked as valid

## Troubleshooting

- **TLS/SSL Certificate Error:** Use `--insecure` flag with Newman (development only) or set proper CA certificates
- **baseUrl not updating:** Ensure you're editing the collection-level variable, not request-level
- **Tests failing:** Verify the API endpoint matches your `baseUrl` and is accessible from your network

---

Want to generate tests for a specific API? Provide the base URL and endpoint documentation!