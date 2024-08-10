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
git clone https://github.com/patryk-czarnecki/Project3-APITesting.git
```

## How to Run Tests Locally

### Postman

1. Install Postman from [here](https://www.postman.com/downloads/).

2. Import the Postman collection and environment:

   - Open Postman.
   - Click on "Import" and select the exported Postman collection file (e.g., `Postman/collection.json`).
   - Click on "Import" again and select the environment file (e.g., `Postman/environment.json`).

3. Run the collection in Postman.

## Prerequisites

### Install Node.js and npm

If you do not have Node.js and npm installed, download and install them from [here](https://nodejs.org/).

### Newman

#### Install Newman and dependencies:
```Bash
npm install --legacy-peer-deps
```

#### Run the Postman collection with Newman:
```Bash
npm test
```

#### View the report:

After running the tests with Newman, an HTML report will be generated in the `reports` directory.
Open `reports/postman_test_report.html` in a browser to view the test results.

### JMeter

1. Install Apache JMeter from [here](https://jmeter.apache.org/download_jmeter.cgi).

2. Open JMeter and load the test plan file:

   - Launch JMeter.
   - Click on `File > Open`.
   - Navigate to `jmeter/test_plan.jmx` and open it.

3. Run the test plan by clicking on the green "Start" button.

### Jenkinsfile Configuration
```javascript
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/patryk-czarnecki/Project3-APITesting.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --legacy-peer-deps'
            }
        }

        stage('Run Postman Tests') {
            steps {
                sh 'npm test'
            }
        }
        
        stage('Archive Results and Documentation') {
            steps {
                archiveArtifacts artifacts: 'reports/*.html'                
            }
        }
    }

    post {
        always {
            publishHTML(target: [
                allowMissing: false,
                alwaysLinkToLastBuild: true,
                keepAll: true,
                reportDir: 'reports',
                reportFiles: 'postman_test_report.html',
                reportName: 'Postman Test Report'
            ])            
        }
    }
}
```
### Jenkins and Node.js Configuration using the NodeJS Plugin

#### Installing Jenkins on Docker

1. **Download and run the Jenkins container:**
   ```bash
   docker run -d --name jenkins -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
   

2. **Obtain the initial admin password:**
   ```bash
   docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
  
3. **Open a browser and go to http://localhost:8080. Enter the initial admin password, install suggested plugins, and create an admin account.**

#### Installing the NodeJS Plugin in Jenkins

1. **Log in to Jenkins:**
Go to [http://localhost:8080](http://localhost:8080) and log in with the admin account.

2. **Install the NodeJS plugin:**

- Navigate to `Manage Jenkins > Plugins`.
- Search for `NodeJS Plugin` in the `Available` tab and install the plugin.

3. **Configure the NodeJS plugin:**

- Go to `Manage Jenkins > Tools`.
- In the `NodeJS` section, click `Add`.
- Name it and select the version of Node.js that matches the version installed on your local machine.
- Check the `Install automatically` option.

### How to Run Tests in Jenkins

1. **Ensure Jenkins is installed and running.**

2. **Create a New Pipeline Job:**
   - Go to Jenkins Dashboard.
   - Click on `New Item`, enter a name for your job, select `Pipeline`, and click `OK`.

3. **Configure the Pipeline:**
   - In the job configuration page, scroll down to the `Pipeline` section.
   - Choose `Pipeline script from SCM` in the `Definition` dropdown.
   - Select `Git` in the `SCM` dropdown.
   - In the `Repository URL` field, enter the URL of the GitHub repository: `https://github.com/patryk-czarnecki/Project3-APITesting.git`.
   - Specify the branch to build: `main`.

4. **Save and Run the Job:**
   - Click `Save` to save the job configuration.
   - To run the job, click `Build Now` in the job dashboard.

## Test Reports

- **[Postman Test Report](./reports/postman_test_report.html)**
- **[JMeter Test Report](./jmeter/results/jmeter_test_report.csv)**

## Conclusion
This project demonstrates how to automate API testing and monitor API performance using Postman, JMeter, and Jenkins. Automating API tests allows for quick and efficient detection of errors and ensures the stability and performance of the tested API.

