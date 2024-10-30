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

