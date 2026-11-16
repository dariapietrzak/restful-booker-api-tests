# Test plan – Restful Booker API

## Objective

Verify that the booking API handles the full booking lifecycle (create, read, update, delete) correctly, protects write operations with authentication and returns correct status codes and data.

## In scope

- Endpoints: `/ping`, `/auth`, `/booking`, `/booking/{id}`
- Functional testing of CRUD operations
- Authentication and authorization (token in cookie)
- Response validation: status codes, body content, JSON schema, headers
- Negative scenarios: missing token, invalid credentials, non-existing resources

## Out of scope

- Performance and load testing (shared public API)
- Security testing beyond basic authorization checks
- XML responses

## Approach

- Each run creates its own test data with a unique first name, so results do not depend on other users of the public API.
- Requests are chained with collection variables (`token`, `bookingId`, `firstname`).
- Test design techniques: equivalence partitioning (valid / invalid credentials, existing / non-existing IDs), state-based testing (booking created → updated → deleted).

## Entry / exit criteria

- Entry: `GET /ping` returns 201.
- Exit: all test cases executed; every failure analysed and either fixed in the tests or documented in [bug-reports.md](bug-reports.md).

## Environment

| Item | Value |
|---|---|
| Base URL | https://restful-booker.herokuapp.com |
| Tools | Postman, Newman, GitHub Actions |
| Test data | Created by the tests at runtime |
