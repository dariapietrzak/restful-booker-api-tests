# Test cases

| ID | Title | Request | Expected result | Type |
|---|---|---|---|---|
| TC-01 | Ping returns 201 | `GET /ping` | 201, response time < 3 s | Smoke |
| TC-02 | Create token with valid credentials | `POST /auth` (admin / password123) | 200, non-empty `token` | Positive |
| TC-03 | Invalid credentials | `POST /auth` (wrong password) | `reason: "Bad credentials"`, no token | Negative |
| TC-04 | Create booking with valid data | `POST /booking` | 200, numeric `bookingid`, returned data equals request, valid JSON schema | Positive |
| TC-05 | Get created booking by ID | `GET /booking/{id}` | 200, JSON, first name as created | Positive |
| TC-06 | Search bookings by first name | `GET /booking?firstname=` | 200, list contains created `bookingid` | Positive |
| TC-07 | Full update with token | `PUT /booking/{id}` + cookie token | 200, updated last name and price | Positive |
| TC-08 | Update without token | `PUT /booking/{id}` | 403 Forbidden | Negative |
| TC-09 | Delete booking with token | `DELETE /booking/{id}` + cookie token | 201 (API convention) | Positive |
| TC-10 | Get deleted booking | `GET /booking/{id}` | 404 Not Found | Negative |
| TC-11 | Get non-existing booking | `GET /booking/999999999` | 404 Not Found | Negative |
