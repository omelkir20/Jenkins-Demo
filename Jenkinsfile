pipeline {
    agent any

    tools {
        maven 'maven-3.5.2'
    }

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

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devopsexample:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh 'docker rm -f devopsexample || true'
                sh 'docker run --name devopsexample -d -p 2222:2222 devopsexample:${BUILD_NUMBER}'
            }
        }
    }

    post {
        success {
            echo 'Pipeline réussi ✅'
        }
        failure {
            echo 'Pipeline échoué ❌'
        }
    }
}
