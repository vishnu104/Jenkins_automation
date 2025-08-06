pipeline {
    agent any

//comment-1
    environment {
        APP_NAME = "my-web-app"
        DOCKER_REGISTRY = "myregistry.com"
    }
//comment-2
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
//comment-3
        stage('Build') {
            steps {
                echo "Building application for branch: ${env.BRANCH_NAME}"
                sh './build.sh'
            }
        }
//comment-4
        stage('Test') {
            steps {
                echo "Running tests for branch: ${env.BRANCH_NAME}"
                sh './test.sh'
            }
        }
//comment-5
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
//comment-6
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
