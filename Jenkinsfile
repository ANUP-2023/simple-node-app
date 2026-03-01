pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "yourdockerhubusername/simple-node-app"
        DOCKER_CREDS = credentials('jenkins-docker')
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'dev',
                    url: 'https://github.com/YOUR_GITHUB/simple-node-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Login to DockerHub') {
            steps {
                sh '''
                echo $DOCKER_CREDS_PSW | docker login \
                -u $DOCKER_CREDS_USR --password-stdin
                '''
            }
        }

        stage('Push Docker Image') {
            steps {
                sh 'docker push $DOCKER_IMAGE:latest'
            }
        }
    }
}
