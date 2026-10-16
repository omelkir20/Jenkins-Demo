pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/omelkir20/Jenkins-Demo.git'
            }
        }

        stage('Build App') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Build image') {
            steps {
                sh 'docker build -t demo-jenkins:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy Docker container') {
            steps {
                sh 'docker rm -f demo-jenkins || true'
                sh 'docker run --name demo-jenkins -d -p 2222:2222 demo-jenkins:${BUILD_NUMBER}'
            }
        }
    }

    post {
        success {
            echo 'Pipeline execution successful! ✅'
        }
        failure {
            echo 'Pipeline execution failed. ❌'
        }
    }
}
