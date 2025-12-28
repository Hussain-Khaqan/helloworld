pipeline {
    agent any

    environment {
        NODE_VERSION = '16'
        APP_ENV = 'development'
    }

    parameters {
        booleanParam(
            name: 'executeTests', 
            defaultValue: true, 
            description: 'Run the Test stage?'
        )
    }

    stages {
        stage('Build') {
            steps {
                echo "=== Building Project ==="
                echo "Node Version: ${env.NODE_VERSION}"
                echo "Environment: ${env.APP_ENV}"

                script {
                    if (isUnix()) {
                        sh "echo Installing Node ${env.NODE_VERSION}"
                        sh "nvm install ${env.NODE_VERSION} || true"
                        sh "node -v"
                    } else {
                        bat "echo Installing Node ${env.NODE_VERSION}"
                        // Windows users need NVM for Windows or skip Node commands
                    }
                }
            }
        }

        stage('Test') {
            when {
                expression { return params.executeTests }
            }
            steps {
                echo "=== Running Tests ==="
                script {
                    if (isUnix()) {
                        sh "echo Running tests..."
                    } else {
                        bat "echo Running tests..."
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "=== Deploying Project ==="
                script {
                    if (isUnix()) {
                        sh "echo Deploying to environment: ${APP_ENV}"
                    } else {
                        bat "echo Deploying to environment: %APP_ENV%"
                    }
                }
            }
        }
    }
}
