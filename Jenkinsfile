@Library('shared') _

pipeline {
    agent { label 'slave' }

    stages {
        stage('Version Calculation') {
            steps {
                script {
                    // Get current build number
                    def buildNumber = env.BUILD_NUMBER.toInteger()
                    
                    // Calculate major and minor versions
                    def majorVersion = Math.floor(buildNumber / 50)
                    def minorVersion = buildNumber % 50
                    
                    // Format minor version with leading zero if needed
                    def formattedMinor = String.format("%02d", minorVersion)
                    
                    // Create the tag
                    def imageTag = "${majorVersion}.${formattedMinor}"
                    
                    // Store in environment variable
                    env.IMAGE_TAG = imageTag
                }
            }
        }
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
                sh 'cd frontend && docker build -t ebadarshad/school-frontend:${env.IMAGE_TAG} .'
                sh 'cd backend && docker build -t ebadarshad/school-backend:${env.IMAGE_TAG} .'
                echo 'Build images successful'
            }
        }
        // stage('Security Scan with Trivy') {
        //     steps {
        //         sh 'trivy image ebadarshad/school-frontend:latest'
        //     }
        // }
        stage('Push image to DockerHub') {
            steps {
                echo 'This is Dockerhub image push stage'
                sh 'docker push ebadarshad/school-frontend:${env.IMAGE_TAG}'
                sh 'docker push ebadarshad/school-backend:${env.IMAGE_TAG}'
                echo 'Pushed image to Dockerhub'
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is deploy stage'
                sh 'docker compose down'
                sh 'APP_VERSION=${env.IMAGE_TAG} docker compose up --build -d'
                echo "Deployed version: ${env.IMAGE_TAG}"
            }
        }
    }
}
