# Creating a CI/CD Pipeline using Azure DevOps

### Step 1: Set Up Your Environment

1. **Create an Azure DevOps Account**:
   - Go to [Azure DevOps](https://dev.azure.com/).
   - Sign up for a free account if you don't already have one.

2. **Create a New Project**:
   - Once logged in, click on `New Project`.
   - Enter the project name, description, and visibility (public or private).
   - Click on `Create`.

### Step 2: Set Up a Git Repository

1. **Create a Repository**:
   - Inside your project, navigate to `Repos` and click on `Initialize`.
   - This will create a new Git repository for your project.

2. **Clone the Repository**:
   - Clone the repository to your local machine using the URL provided by Azure DevOps.
   - Use the following command in your terminal:
     ```sh
     git clone https://dev.azure.com/your-organization/your-project/_git/your-repo
     cd your-repo
     ```

### Step 3: Set Up a Simple Application

1. **Create a Simple Web Application**:
   - For this example, let's use a simple Node.js application.
   - Create the following files in your repository:
     - `app.js`:
       ```js
       const http = require('http');

       const hostname = '127.0.0.1';
       const port = 3000;

       const server = http.createServer((req, res) => {
         res.statusCode = 200;
         res.setHeader('Content-Type', 'text/plain');
         res.end('Hello World\n');
       });

       server.listen(port, hostname, () => {
         console.log(`Server running at http://${hostname}:${port}/`);
       });
       ```

     - `package.json`:
       ```json
       {
         "name": "simple-node-app",
         "version": "1.0.0",
         "description": "A simple Node.js web server",
         "main": "app.js",
         "scripts": {
           "start": "node app.js"
         },
         "author": "",
         "license": "ISC",
         "dependencies": {
           "express": "^4.17.1"
         }
       }
       ```

2. **Install Dependencies**:
   - Run the following command to install the necessary dependencies:
     ```sh
     npm install
     ```

3. **Push the Code to the Repository**:
   - Add and commit your changes:
     ```sh
     git add .
     git commit -m "Initial commit"
     git push origin master
     ```

### Step 4: Set Up the CI/CD Pipeline

1. **Create a Build Pipeline**:
   - In Azure DevOps, navigate to `Pipelines` and click on `New Pipeline`.
   - Select your repository (the one you created and pushed your code to).
   - Choose `Node.js` as the template.

2. **Configure the Pipeline**:
   - Azure DevOps will generate a basic `azure-pipelines.yml` file. Modify it as follows:
     ```yaml
     trigger:
       - master

     pool:
       vmImage: 'ubuntu-latest'

     steps:
     - task: UseNode@1
       inputs:
         version: '10.x'

     - script: |
         npm install
         npm test
       displayName: 'Install dependencies and run tests'

     - script: npm start
       displayName: 'Start Application'
     ```

3. **Save and Run the Pipeline**:
   - Save the `azure-pipelines.yml` file and commit it to your repository.
   - The pipeline will automatically trigger and run the steps defined.

### Step 5: Continuous Deployment

1. **Set Up a Release Pipeline**:
   - Navigate to `Pipelines` > `Releases` and click on `New Release Pipeline`.
   - Select the `Azure App Service deployment` template.

2. **Configure the Stages**:
   - Add an artifact from your build pipeline.
   - Define the stage to deploy to Azure App Service.

3. **Set Up Azure App Service**:
   - If you don't have an Azure App Service set up, create one in the Azure Portal.
   - Connect your Azure DevOps project to your Azure subscription.

4. **Deploy the Application**:
   - Configure the release pipeline to deploy the build artifact to Azure App Service.
   - Create a release and deploy your application.

### Step 6: Monitor and Maintain

1. **Monitor the Pipeline**:
   - Use Azure DevOps to monitor the status of your builds and releases.
   - Set up alerts for failed builds or deployments.

2. **Iterate and Improve**:
   - Continuously improve your pipeline by adding more stages (e.g., testing, staging).
   - Automate more tasks as you become more comfortable with Azure DevOps.

### Summary

This project will demonstrate your ability to set up and manage a complete CI/CD pipeline, showcasing your skills in automation, cloud services, and DevOps practices.