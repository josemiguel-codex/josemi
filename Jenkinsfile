pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git 'https://github.com/josemiguel-codex/proyecto-ci-cd-hiro.git'
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
                sh 'docker login -u TU_USUARIO -p TU_PASSWORD'
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
