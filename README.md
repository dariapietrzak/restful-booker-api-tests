# Restful Booker – REST API tests

![API tests](https://github.com/dariapietrzak/restful-booker-api-tests/actions/workflows/api-tests.yml/badge.svg)

API test suite for [Restful Booker](https://restful-booker.herokuapp.com/apidoc/index.html), a public practice API for hotel bookings. The project covers test design, Postman tests, JSON schema validation, negative testing and automated runs in CI with Newman and GitHub Actions.

## Scope

| Area | Endpoints | What is checked |
|---|---|---|
| Health check | `GET /ping` | Availability and response time |
| Authentication | `POST /auth` | Token for valid credentials, error for invalid ones |
| Create | `POST /booking` | Status, returned data vs request body, JSON schema |
| Read | `GET /booking/{id}`, `GET /booking?firstname=` | Data of the created booking, search by name |
| Update | `PUT /booking/{id}` | Update with token, 403 without token |
| Delete | `DELETE /booking/{id}` | Deletion with token, 404 after deletion |
| Negative | `GET /booking/{id}` | 404 for a non-existing booking |

Full list: [docs/test-cases.md](docs/test-cases.md) · Approach: [docs/test-plan.md](docs/test-plan.md) · Findings: [docs/bug-reports.md](docs/bug-reports.md)

## Test flow

The tests run as one end-to-end scenario and pass data between requests with collection variables:

```
POST /auth ──► token
POST /booking ──► bookingId
GET /booking/{bookingId} ──► verify data
PUT /booking/{bookingId} (token) ──► verify update
DELETE /booking/{bookingId} (token) ──► GET returns 404
```

## Tech stack

- Postman (collections, environments, `pm.test` assertions, JSON schema validation)
- Newman (command-line runner)
- GitHub Actions (runs on every push, pull request and weekly; HTML report saved as a build artifact)

## How to run

**In Postman:** import both files from the `postman/` folder, select the *Restful Booker – public* environment and run the collection with Collection Runner.

**From the command line:**

```bash
npm install -g newman newman-reporter-htmlextra
newman run postman/restful-booker.postman_collection.json \
  -e postman/restful-booker.postman_environment.json \
  --reporters cli,htmlextra
```

The HTML report is saved in the `newman/` folder.

## Notes

- Restful Booker is a shared public API that is reset regularly, so the tests create their own data and do not rely on existing bookings.
- The credentials in the environment file are the public demo credentials published in the API documentation.

## Author

Daria Pietrzak, Manual QA Engineer (ISTQB CTFL) · [LinkedIn](https://www.linkedin.com/in/dariapietrzak1990)
