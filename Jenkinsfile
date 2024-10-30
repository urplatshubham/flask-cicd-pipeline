pipeline {
    agent any

    environment {
        // Define environment variables for staging and production messages
        STAGING_MESSAGE = "Simulating staging deployment"
        PRODUCTION_MESSAGE = "Simulating production deployment"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Checking out code...'
                // Manually clone the repository
                sh 'git clone https://github.com/urplatshubham/flask-cicd-pipeline .'
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
                    echo "Build stage complete"
                '''
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'staging' // Only run when pushing to the staging branch
            }
            steps {
                echo 'Deploying to staging environment...'
                echo "${STAGING_MESSAGE}"
            }
        }

        stage('Deploy to Production') {
            when {
                // Only run on tagged commits with pattern vX.Y (e.g., v1.0)
                expression { return env.GIT_TAG_NAME ==~ /^v[0-9]+(\\.[0-9]+)*$/ }
            }
            steps {
                echo 'Deploying to production environment...'
                echo "${PRODUCTION_MESSAGE}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs for details.'
        }
    }
}
