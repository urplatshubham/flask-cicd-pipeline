# flask-cicd-pipeline
## GitHub Actions CI/CD Workflow

This repository includes a CI/CD pipeline using GitHub Actions.

### Workflow Overview
1. **Install Dependencies**: Installs required Python packages.
2. **Run Tests**: Runs unit tests using pytest.
3. **Build**: Builds the application if tests pass.
4. **Deploy to Staging**: Simulates deployment to staging when changes are pushed to the `staging` branch.
5. **Deploy to Production**: Simulates deployment to production on tagged releases (e.g., `v1.0`).

### Running the Workflow
- The workflow automatically triggers on pushes to `staging`, pull requests to `main`, and on versioned tags (e.g., `v1.0`) for production.

> **Note**: Deployment steps are simulated for demonstration and do not require actual deployment keys.
To set up a similar CI/CD pipeline for a Flask application using Jenkins, here’s a step-by-step guide. This setup includes Jenkins stages for installing dependencies, running tests, building, and simulating deployments to both staging and production environments, all without requiring real servers or credentials.

### 1. Set Up a Jenkins Pipeline Job

1. **Access Jenkins**: Open Jenkins and log in.
2. **Create a New Pipeline Job**:
   - Go to **New Item** > **Pipeline**, and name it (e.g., `flask-cicd-pipeline`).
3. **Configure the Pipeline**:
   - In the job configuration, scroll down to the **Pipeline** section.
   - Select **Pipeline script** and paste in the pipeline code (detailed below).

### 2. Jenkinsfile: Define the Pipeline Stages
In your repository, create a `Jenkinsfile` in the root directory. This file will define the stages for your CI/CD pipeline. Here’s an example Jenkinsfile for the Flask app:

```groovy
pipeline {
    agent any

    environment {
        // Define environment variables for staging and production
        STAGING_ENV = "Simulating staging deployment"
        PRODUCTION_ENV = "Simulating production deployment"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh '''
                # Placeholder for build commands
                echo "Build complete"
                '''
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'staging'
            }
            steps {
                echo 'Deploying to staging environment...'
                echo "${STAGING_ENV}"
            }
        }

        stage('Deploy to Production') {
            when {
                expression { return env.GIT_TAG_NAME ==~ /^v[0-9]+(\\.[0-9]+)*$/ }
            }
            steps {
                echo 'Deploying to production environment...'
                echo "${PRODUCTION_ENV}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs for details.'
        }
    }
}
```

### 3. Explanation of Each Stage

- **Checkout Code**: Pulls the code from the repository.
- **Install Dependencies**: Creates a Python virtual environment and installs dependencies.
- **Run Tests**: Activates the environment and runs `pytest` to execute tests.
- **Build**: Simulates a build stage (can be extended with actual build commands).
- **Deploy to Staging**: Deploys to staging when the `staging` branch is built.
- **Deploy to Production**: Deploys to production when a tagged release with the pattern `v*.*` (e.g., `v1.0`) is built.

### 4. Configuring Branch and Tag-Based Triggers

To trigger this pipeline based on specific branches or tags:
1. In the Jenkins job configuration, go to **Build Triggers**.
2. Enable **Poll SCM** or set up a **Webhook** in GitHub that points to your Jenkins job.
3. For tag-based builds, Jenkins needs to detect the tag. Ensure your source control management configuration includes tag polling.

### 5. Environment Variables
- **STAGING_ENV** and **PRODUCTION_ENV**: These environment variables hold messages for simulating staging and production deployments. They’re printed in the relevant stages to demonstrate where a real deployment would occur.

### 6. Test the Pipeline

1. **Push Changes to the Staging Branch**:
   - Make a small update in the `staging` branch, and push it to trigger the staging deployment.
2. **Tag a Release**:
   - Tag the main branch with a version number (e.g., `v1.0`) and push it to trigger the production deployment.

You should see each stage complete in the Jenkins console log, with “Simulating staging deployment” or “Simulating production deployment” printed for the respective deployment stages.

### Sample README for Jenkins CI/CD Pipeline

Here's a README description for documenting this pipeline setup:

---

# Flask CI/CD Pipeline with Jenkins

This repo contains a simple Flask application and a Jenkins pipeline that performs basic CI/CD operations – including dependency installation, testing, building, and simulating deployments.

## Overview

The pipeline performs these steps:
1. **Checkout Code**: Retrieves the latest code from the repository.
2. **Install Dependencies**: Sets up a Python virtual environment and installs the required packages.
3. **Run Tests**: Runs unit tests with pytest.
4. **Build**: Placeholder build step, simulating preparation for deployment.
5. **Deploy to Staging**: Simulates staging deployment when code is pushed to the `staging` branch.
6. **Deploy to Production**: Simulates production deployment when a version tag (e.g., `v1.0`) is pushed.

### Getting Started

To run the app locally:
```bash
pip install -r requirements.txt
python app.py
```

### Setting Up the Jenkins Pipeline

1. **Create a new Pipeline job** in Jenkins.
2. **Add a Jenkinsfile** to the root of this repository.
3. **Configure the Jenkins job** to trigger on changes to the `staging` branch or when a version tag is pushed.

### Pipeline Stages

- **Install Dependencies**: Sets up the app with necessary packages.
- **Run Tests**: Executes basic tests to verify functionality.
- **Build**: Placeholder build stage to demonstrate progress.
- **Deploy to Staging**: Runs only on `staging` branch pushes.
- **Deploy to Production**: Runs only on version tags.

> **Note**: This pipeline only simulates deployment steps and does not require actual deployment keys.

### Running the Pipeline

Trigger the pipeline manually or by pushing code to `staging` or tagging a release.
