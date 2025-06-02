pipeline {
    agent any

    environment {
        IMAGE_NAME = 'renuka1217/sales-module'
        IMAGE_TAG = 'latest'
        DOCKER_USER = 'renuka1217'
        DOCKER_PASS = 'LMC86_pnsGmk?5Q'

    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/renuka1217/devops_practice-june.git'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
                // Add build steps like `mvn clean install` or `npm install`
            }
        }
        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhubcredentials',
                    usernameVariable: 'renuka1217',
                    passwordVariable: 'LMC86_pnsGmk?5Q'
                )]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    '''
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
                // Add test commands
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying...'
                // Add deployment logic
            }
        }
    }
}

