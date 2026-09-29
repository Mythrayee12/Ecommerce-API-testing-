# Ecommerce API Testing with Postman

## Overview

This project demonstrates REST API testing for an e-commerce application using Postman.

The collection covers authentication, authenticated API requests, product retrieval, product creation, product update, product deletion, environment variables, request chaining, and response validation.

The project focuses on practical API testing and QA fundamentals, including HTTP methods, JSON request and response handling, authentication, dynamic variables, and automated assertions.

## Tools and Technologies

* Postman
* REST APIs
* HTTP
* JSON
* JavaScript
* Git
* GitHub

## Project Structure

```text
Ecommerce-API-testing/
│
├── README.md
│
├── collections/
│   └── Ecommerce_API_Project.json
│
├── environments/
│   └── Ecommerce_Environment.json
│
├── test-cases/
│
├── screenshots/
│
└── reports/
```

## API Coverage

### Authentication

The project includes a login API for obtaining an authentication token.

* Login using valid credentials
* Extract the access token from the response
* Store the token as a Postman environment variable
* Use the token for authenticated requests

The login request stores the returned `accessToken` in the `token` environment variable.

### User API

#### Get User Profile

The User Profile API demonstrates an authenticated request using a Bearer token.

* Sends the stored authentication token
* Retrieves the authenticated user's profile
* Validates the HTTP response status

The request uses the `token` environment variable as Bearer authentication.

### Product APIs

The project currently covers the following product operations:

* Get all products
* Get a single product
* Add a product
* Update an existing product
* Delete an existing product

## HTTP Methods

| Method | API Operation      | Purpose                     |
| ------ | ------------------ | --------------------------- |
| POST   | Login              | Authenticate user           |
| POST   | Get User Profile   | Retrieve authenticated user |
| GET    | Get Products       | Retrieve product list       |
| GET    | Get Single Product | Retrieve a specific product |
| POST   | Add Product        | Create a product            |
| PUT    | Update Product     | Update an existing product  |
| DELETE | Delete Product     | Delete an existing product  |

## Product API Workflow

```text
Login API
    |
    v
Store Authentication Token
    |
    v
Get User Profile
    |
    v
Get Products
    |
    v
Store First Product ID
    |
    v
Get Single Product
    |
    v
Add Product
    |
    v
Update Existing Product
    |
    v
Delete Existing Product
```

## Environment Variables

The collection uses Postman environment variables to avoid hardcoding dynamic values.

Current variables include:

```text
base_url
token
firstProductId
createdProductId
```

### Token

The Login API extracts the `accessToken` from the response and stores it in the `token` environment variable.

### Product ID

The Get Products request extracts the ID of the first product and stores it as:

```text
firstProductId
```

This value is then used by the Get Single Product request.

## Test Assertions

Postman test scripts are used to validate API responses.

Current assertions include:

* HTTP status code validation
* JSON response validation
* Product ID validation
* Product title validation
* Product price validation

Example:

```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response is JSON", function () {
    pm.response.to.be.json;
});

const data = pm.response.json();

pm.test("Product ID exists", function () {
    pm.expect(data.id).to.exist;
});
```

The Add Product request currently validates the status code, JSON response, product ID, product title, and product price.

## CRUD Testing

The project demonstrates the basic CRUD operations:

### Create

```text
POST /products/add
```

A product is submitted using a JSON request body containing:

* Title
* Price
* Description
* Category

### Read

```text
GET /products
GET /products/{productId}
```

The first endpoint retrieves the product list, while the second retrieves an individual product.

### Update

```text
PUT /products/{productId}
```

An existing product is updated with modified product information.

### Delete

```text
DELETE /products/{productId}
```

An existing product is deleted using its product ID.

## Request Data

Example product request:

```json
{
    "title": "Test Laptop",
    "price": 999,
    "description": "Laptop created through Postman",
    "category": "electronics"
}
```

The Add Product request uses this JSON payload in the current collection.

## API Behavior Observed

During testing, the Add Product endpoint returned a generated product ID in the response.

However, the newly created product was not persisted by the demo API. As a result, the generated ID could not subsequently be used reliably for Update or Delete operations.

For Update and Delete testing, an existing product ID is used instead.

This behavior is documented as a limitation of the demo/test API rather than being treated as a Postman configuration issue.

## Current Testing Scope

The current version of the project covers:

* REST API request creation
* HTTP methods
* Authentication
* Bearer token authentication
* Environment variables
* Dynamic product IDs
* Request chaining
* JSON request bodies
* Response validation
* Status code validation
* CRUD operations
* API behavior documentation

The project does not currently claim dedicated positive, negative, or boundary-value test suites.

## Future Enhancements

The following features can be added in future iterations:

* Negative API test scenarios
* Boundary-value testing
* Invalid authentication testing
* Invalid request-data testing
* Error-response validation
* More comprehensive response assertions
* Data-driven testing
* Postman Collection Runner execution
* Newman command-line execution
* Automated test reports
* API schema validation
* Response-time assertions
* Database validation
* GitHub Actions CI/CD integration
* Automated regression testing

## How to Run

1. Clone the repository.
2. Open Postman.
3. Import `collections/Ecommerce_API_Project.json`.
4. Import the environment from the `environments` directory.
5. Select the imported environment.
6. Verify the `base_url` and required variables.
7. Run the Login API first to generate the authentication token.
8. Execute the remaining requests individually or run the collection.
9. Review the response and Postman test results.

## Test Execution Flow

```text
Environment Setup
       |
       v
Login API
       |
       v
Authentication Token
       |
       v
User Profile
       |
       v
Product Retrieval
       |
       v
Product CRUD
       |
       v
Response Validation
       |
       v
Test Results
```

## Project Objective

The objective of this project is to demonstrate practical knowledge of REST API testing using Postman, including API request creation, authentication, environment management, request chaining, CRUD operations, response validation, and documentation of observed API behavior.

## Author

**Mythrayee**

Computer Science Undergraduate | QA & Automation | AI/ML Enthusiast

## Disclaimer

This project uses a demo/test API for learning and API testing purposes. API behavior, persistence, availability, and response formats may differ from those of a production e-commerce application.
