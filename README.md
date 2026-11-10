# RESTful Booker API Testing — Postman

A practical API testing project using **Postman** and the public [RESTful Booker](https://restful-booker.herokuapp.com/apidoc/index.html) demo API. Covers manual and automated API checks without relying on a UI.

## Features

- **CRUD workflow:** authenticate, create booking, GET booking, PATCH, PUT, and DELETE.
- **Request chaining:** extract authentication token and booking ID for subsequent requests.
- **Positive tests:** status codes, response fields, business expectations, and JSON Schema validation.
- **Negative tests:** invalid booking ID (404), invalid token (403), and missing required fields (the demo API has previously returned 500, a potential validation defect).
- **Data-driven tests:** three sets of booking inputs using pre-request scripts and three Runner iterations, without a paid CSV feature.

## Reported test result

**20/20 tests passed, 0 failed, 0 errors** in one Postman Collection Runner execution of the six-request Core CRUD Flow on November 10, 2026 (as shown in the project screenshot). This is a manually observed result, **not** an automatically executed GitHub CI check. The negative and data-driven folders are separate runs.

## Run locally

1. Import [the Postman collection](API_Chaining_Project.postman_collection.json) into Postman.
2. Open the collection's **Variables** and check `baseUrl` is `https://restful-booker.herokuapp.com`.
3. Run **Core CRUD Flow - Run in order** with **1 iteration**. Order matters: GET must happen before updates and DELETE.
4. Run **Negative Tests** separately. For invalid-token PATCH, create a fresh booking first so the ID exists. The missing-fields contract test may intentionally fail when the server responds 500 instead of 4xx.
5. Run **Data Driven - Run 3 iterations** with **3 iterations** (no CSV required).

The scripts save `token` and `bookingId` to collection variables and, for compatibility with the earlier local Postman workspace, also to global variables. Avoid sharing real credentials or secrets; demo credentials in this collection are public test credentials. If variables are unresolved, check their scope and values before running.

## Tech stack

Postman · JavaScript assertions (`pm.test`) · HTTP · JSON · REST APIs · GitHub

## Project structure

```text
API_Chaining_Project.postman_collection.json
README.md
```

## Notes

This repository contains a reconstructed version of the tested Postman workflow, not a direct export from the local Postman workspace. Re-run the imported collection to verify behavior in your environment. Public demo API responses and availability can vary.
