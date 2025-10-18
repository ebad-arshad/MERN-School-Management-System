pipeline {
    agent { label "slave" }

    stages {
        stage('Code') {
            steps {
                echo 'This is code stage'
                git url:"https://github.com/ebad-arshad/MERN-School-Management-System", branch:"main"
                echo 'Cloned successfully'
            }
        }
        stage('Login DockerHub') {
            steps {
                echo 'This is Dockerhub login stage'
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                  sh 'docker login -u $USERNAME -p $PASSWORD'
                }
                echo 'Login to Dockerhub'
            }
        }
        stage('Push image to DockerHub') {
            steps {
                echo 'This is Dockerhub image push stage'
                sh 'cd frontend && docker build -t ebadarshad/school-frontend:latest .'
                sh 'cd backend && docker build -t ebadarshad/school-backend:latest .'
                sh 'docker push ebadarshad/school-frontend:latest && docker push ebadarshad/school-backend:latest'
                echo 'Pushed image to Dockerhub'
            }
        }
        stage('Build') {
            steps {
                echo 'This is build stage'
                
            }
        }
        stage('Test') {
            steps {
                echo 'This is test stage'
            }
        }
        stage('Deploy') {
            steps {
                echo 'This is deploy stage'
                sh "docker compose up --build -d"
                echo 'Deployment completed'
            }
        }
        
    }
}
