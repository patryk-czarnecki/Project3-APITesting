# Project 3: API Testing with Postman and JMeter

## Description
This project involves testing the JSONPlaceholder API using Postman and JMeter. The tests focus on various HTTP methods and validating the responses as well as performance testing.

## Test Plan

### Description
The objective of this project is to verify the functionality and performance of the JSONPlaceholder API. The tests focus on various endpoints and methods such as GET, POST, PUT, and DELETE.

### Scope of Testing

1. **GET /posts**: Retrieve a list of posts.
2. **GET /posts/:id**: Retrieve a specific post by ID.
3. **POST /posts**: Create a new post.
4. **PUT /posts/:id**: Update an existing post by ID.
5. **DELETE /posts/:id**: Delete a post by ID.

### Testing Environment

- **Tool**: Postman, JMeter

### Types of Tests

1. **Functional Tests**: To verify that each endpoint works according to the requirements.
2. **Performance Tests**: To evaluate the performance and scalability of the API.

## How to Run Tests Locally

### Postman

1. Install Postman from [here](https://www.postman.com/downloads/).

2. Import the Postman collection:

   - Open Postman.
   - Click on "Import" and select the exported Postman collection file (e.g., `Postman/collection.json`).

3. Run the collection in Postman.

### Newman

1. Install Newman:

   ```bash
   npm install -g newman
   ```

2. Run the Postman collection with Newman:
   
   ```bash
   npx newman run Postman/collection.json -r html --reporter-html-export reports/postman_test_report.html
   ```

### JMeter

1. **Install Apache JMeter from [here](https://jmeter.apache.org/download_jmeter.cgi).**

2. **Open JMeter and load the test plan file (e.g., `test_plan.jmx`).**

3. **Run the test plan.**

## Test Reports

- [Postman Test Report](reports/postman_test_report.html)
- [JMeter Test Report](reports/jmeter_test_report.html)

## Screenshots
