pipeline {
    agent any

    environment {
        IMAGE_NAME = "weather-app"
        CONTAINER_NAME = "weather-container"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/sravanthisaginala2004/weatherapp'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t $IMAGE_NAME .'
                    } else {
                        powershell 'docker build -t $env:IMAGE_NAME .'
                    }
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                        docker stop $CONTAINER_NAME || true
                        docker rm $CONTAINER_NAME || true
                        docker run -d -p 8000:8000 --name $CONTAINER_NAME $IMAGE_NAME
                        '''
                    } else {
                        powershell '''
                        docker stop $env:CONTAINER_NAME -ErrorAction SilentlyContinue
                        docker rm $env:CONTAINER_NAME -ErrorAction SilentlyContinue
                        docker run -d -p 8000:8000 --name $env:CONTAINER_NAME $env:IMAGE_NAME
                        '''
                    }
                }
            }
        }
    }
}
