# Project 3: API Testing with Postman, Newman, JMeter, and Jenkins

## Description
This project involves testing the JSONPlaceholder API using Postman, Newman, JMeter, and Jenkins. The tests focus on various HTTP methods and validating the responses as well as performance testing.

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

- **Tools**: Postman, Newman, JMeter, Jenkins

### Types of Tests

1. **Functional Tests**: To verify that each endpoint works according to the requirements.
2. **Performance Tests**: To evaluate the performance and scalability of the API.

### Detailed Test Cases

#### GET /posts
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Response has JSON body", function () {
    pm.response.to.be.json;
});

pm.test("Response contains posts", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.be.an('array').that.is.not.empty;
});
```
   
#### POST /posts
```javascript
pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Response has JSON body", function () {
    pm.response.to.be.json;
});

pm.test("Response contains created post", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property('id');
    pm.expect(jsonData).to.have.property('title', pm.environment.get("postTitle"));
    pm.expect(jsonData).to.have.property('body', pm.environment.get("postBody"));
    pm.expect(jsonData).to.have.property('userId', parseInt(pm.environment.get("userId")));
});
```

#### GET /posts/1
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Response has JSON body", function () {
    pm.response.to.be.json;
});
```

#### PUT /posts/1
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Response has JSON body", function () {
    pm.response.to.be.json;
});
```

#### DELETE /posts/1
```javascript
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response time is less than 500ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(500);
});

pm.test("Response body is empty JSON object", function () {
    pm.expect(pm.response.json()).to.eql({});
});
```

## How to Clone the Repository

### Clone the repository:
```Bash
git clone https://github.com/yourusername/Project3-APITesting.git
```

## How to Run Tests Locally

### Postman

1. Install Postman from [here](https://www.postman.com/downloads/).

2. Import the Postman collection and environment:

   - Open Postman.
   - Click on "Import" and select the exported Postman collection file (e.g., `Postman/collection.json`).
   - Click on "Import" again and select the environment file (e.g., `Postman/environment.json`).

3. Run the collection in Postman.

### Newman

#### Install Newman and dependencies:
```Bash
npm install --legacy-peer-deps
```

#### Run the Postman collection with Newman:
```Bash
npm test
```

### View the report:

After running the tests with Newman, an HTML report will be generated in the `reports` directory.
Open `reports/postman_test_report.html` in a browser to view the test results.

### JMeter

1. Install Apache JMeter from [here](https://jmeter.apache.org/download_jmeter.cgi).

2. Open JMeter and load the test plan file:

   - Launch JMeter.
   - Click on `File > Open`.
   - Navigate to `jmeter/test_plan.jmx` and open it.

3. Run the test plan by clicking on the green "Start" button.

### How to Run Tests in Jenkins

1. Ensure Jenkins is installed and running.

2. Create a new Jenkins job:

   - Go to Jenkins and create a new "Pipeline" job.
   - Configure the job to use the GitHub repository where this project is hosted.

3. Run the pipeline:

   - Manually trigger the job or configure a webhook to automatically trigger it after each push.

4. View the report:

   - After the pipeline completes, go to the "Postman Test Report" tab in Jenkins to see the test results.

## Test Reports

- **Postman Test Report**: `reports/postman_test_report.html`
- **JMeter Test Report**: `jmeter/results/jmeter_test_report.csv`

## Conclusion
This project demonstrates how to automate API testing and monitor API performance using Postman, JMeter, and Jenkins. Automating API tests allows for quick and efficient detection of errors and ensures the stability and performance of the tested API.

