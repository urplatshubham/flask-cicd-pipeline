# Flask CI/CD Pipeline with GitHub Actions & Jenkins
This repo showcases a simple Flask app and a GitHub Actions workflow & Jenkins that handles basic CI/CD tasks – from installing dependencies to simulating staging and production deployments.

## Overview

This project includes a minimal Flask app with a single route and a GitHub Actions pipeline to automate testing, building, and "deploying" the app (just for show, no actual servers involved).

The workflow covers:
1. **Installing dependencies** – sets up the app with everything it needs to run.
2. **Running tests** – executes basic tests to ensure the app works.
3. **Building the app** – just a placeholder step to show build progress.
4. **Deploying to Staging** – runs if we push code to the `staging` branch.
5. **Deploying to Production** – runs on tagged releases (like `v1.0`) for production.

### Getting Started

If you want to try this out, clone the repo and check out the basic Flask setup in `app.py`. The app’s pretty straightforward; it just returns “Hello, GitHub Actions CI/CD!” on the homepage. There’s also a test in `test_app.py` to keep things honest.

#### Running the App Locally
Make sure you have Python 3.8+ installed. Then install the dependencies:

```bash
pip install -r requirements.txt
```

Run the app:

```bash
python app.py
```

### GitHub Actions Workflow

The real focus here is the GitHub Actions workflow. Here's a rundown of what it does:

- **Install Dependencies**: Sets up Python and installs the requirements.
- **Run Tests**: Runs `pytest` to check if the app is working as expected.
- **Build**: Just a placeholder build step.
- **Deploy to Staging**: Simulated deployment when pushing to `staging` branch.
- **Deploy to Production**: Simulated deployment on a version tag push, e.g., `v1.0`.

### Workflow Triggers
The CI/CD workflow triggers on:

- Pushes to the `staging` branch (to simulate staging deployment).
- Pull requests targeting the `main` branch.
- Versioned tags (like `v1.0`) to simulate production deployment.

### Running the Workflow

Push changes to the `staging` branch to simulate staging deployment, or tag a release (e.g., `v1.0`) to simulate production deployment. The steps will be logged in the **Actions** tab under your repo.

### Important Notes
> **Note**: This pipeline is only a simulation – no actual deployments to staging or production servers happen here, and no secrets are needed.

### Screenshots of Deployment done
![Screenshot (780)](https://github.com/user-attachments/assets/9e556579-2367-4b15-91b7-949f1080324f)
![Screenshot (779)](https://github.com/user-attachments/assets/e2b73aa6-6a61-4469-9b11-14618562d3e9)

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
