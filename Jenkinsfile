pipeline {
    agent any

<<<<<<< HEAD
#comment-1
=======
>>>>>>> bee9f95 (critical fixes in prod branch main by mistake)
    environment {
        APP_NAME = "my-web-app"
        DOCKER_REGISTRY = "myregistry.com"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building application for branch: ${env.BRANCH_NAME}"
                sh './build.sh'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests for branch: ${env.BRANCH_NAME}"
                sh './test.sh'
            }
        }

        stage('Deploy') {
            when {
                branch 'release1'
            }
            steps {
                script {
                    if (env.BRANCH_NAME == 'release1') {
                        echo "Deploying to DEV environment"
                        sh './deploy-dev.sh'
                    } else if (env.BRANCH_NAME == 'qa') {
                        echo "Deploying to QA environment"
                        sh './deploy-qa.sh'
                    } else if (env.BRANCH_NAME == 'prod') {
                        echo "Deploying to PROD environment"
                        sh './deploy-prod.sh'
                    } else {
                        echo "No deployment for this branch"
                    }
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completed for branch: ${env.BRANCH_NAME}"
        }
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Deployment failed!"
        }
    }
}
