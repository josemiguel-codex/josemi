pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Test') {
            steps {
                sh 'pip install flask pytest'
                sh 'pytest'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t josemiguellealroman/flask-app:latest .'
            }
        }

        stage('Push DockerHub') {
            steps {
                sh 'docker login -u josemiguellealroman -p TU_TOKEN'
                sh 'docker push josemiguellealroman/flask-app:latest'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                sh 'kubectl apply -f deployment.yaml'
                sh 'kubectl apply -f service.yaml'
            }
        }

    }
}
