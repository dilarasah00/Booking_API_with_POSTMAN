# Booking API Test Project 


---
> The detailed test cases can be found in the included **Test Cases.xlsx**, which lists all scenarios, steps, expected results, and execution status.

---

### 1. Project Purpose

This project is designed to test the basic CRUD operations and authentication of the Booking API hosted on Heroku.  
The tests cover **positive**, **negative**, and some **edge case** scenarios.

---

### 2. Test Scope

* **Auth**: Obtaining tokens and checking invalid credentials.
* **Booking CRUD**:
  * **Create**: Valid and invalid input tests (empty fields, missing fields, wrong formats)
  * **Read**: Requests with existing, invalid, or deleted IDs
  * **Update**: Valid, missing, invalid token, and incomplete field updates
  * **Delete**: Valid deletion, already deleted records, requests without token, or without ID

---

### 3. Test Status

* Tests are prepared using **Postman**.
* Passed test cases have generally been automated.
* Negative tests mostly remain manual due to API inconsistencies:
  * Status codes and error messages sometimes do not match expected HTTP standards.
  * For example, sending an integer to a string field returns 500, while sending a string to other fields is accepted.


---

### 4. Running Tests


#### Using Postman
Anyone cloning the repository can directly open the Postman collections and environments in Postman and run the tests manually.

```bash
 **Clone the repository**
git clone https://github.com/dilarasah00/Booking_API_with_POSTMAN.git
```


#### Using Newman
To run the tests via **Newman** CLI:

```bash
**Install Newman globally** (if not already installed)
npm install -g newman 
```

```bash
# Run all positive tests
newman run collection/Positive_tests.postman_collection.json \
  -e environment/BookingApi_positiveTest.postman_environment.json \
  -d data/positiveBooking_Data.json
```

```bash
# Run specific folder in negative tests (example: Get Booking)
newman run collection/Negative_tests.postman_collection.json \
  -e environment/BookingApi_negativeTest.postman_environment.json \
  -d data/getBooking_with_invalid_ID.json \
  --folder "Get booking"
```

Other folders in the Negative tests collection can be executed similarly, for example:

- Create token
- Update booking
- Delete booking

> **Note:** In negative tests, different JSON data files are used for each scenario.  
> To understand how these are executed in detail, please refer to the **workflow YAML file** included in `.github/workflows/run_postman_tests.yml`.

---

> Performance tests for the same API are maintained in a separate repository: [Locust Performance Tests](https://github.com/dilarasah00/API-Performance-test-.git)