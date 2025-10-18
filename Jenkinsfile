@Library('shared') _

pipeline {
    agent { label 'slave' }

    stages {
        stage('Clone') {
            steps {
                script {
                    clone('https://github.com/ebad-arshad/MERN-School-Management-System', 'main')
                }
            }
        }
        stage('Login DockerHub') {
            steps {
                script {
                    dockerhub_login('docker-hub-creds')
                }
            }
        }
        stage('Build') {
            steps {
                echo 'This is build stage'
                sh 'cd frontend && docker build -t ebadarshad/school-frontend:latest .'
                sh 'cd backend && docker build -t ebadarshad/school-backend:latest .'
                echo 'Build images successful'
            }
        }
        stage('Push image to DockerHub') {
            steps {
                echo 'This is Dockerhub image push stage'
                sh 'docker push ebadarshad/school-frontend:latest'
                sh 'docker push ebadarshad/school-backend:latest'
                echo 'Pushed image to Dockerhub'
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is deploy stage'
                sh 'docker compose down'
                sh 'docker compose up --build -d'
                echo 'Deployment completed'
            }
        }
    }
}
