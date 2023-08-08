pipeline {
    agent any
    
    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
    }
    
    tools {nodejs "node"}
  
    stages {
    
        stage('Clone Backend Repository') {
            steps {
                // Clone the backend repository
                git branch: 'master', url: 'https://github.com/andynze1/exercise-devops-server.git'
            }
        }

        stage('Build Backend') {
            steps {
                // Install dependencies and build the backend
                sh "cd /home/ubuntu/exercise-devops-server"
                sh "npm install run-s"
                sh "npm install"
                sh "sudo npm install pm2 -g"
            }
        }
        
        stage('Test') {
            steps {
                // Run tests for frontend and backend (modify commands if needed)
                sh "cd /home/ubuntu/exercise-devops-client"
                sh "npm test"
                sh "cd /home/ubuntu/exercise-devops-server && npm test"
            }
        }


    post {
        success {
            script {
                currentBuild.result = 'SUCCESS'
                sh "cd /home/ubuntu/exercise-devops-server"
                sh "pm2 start index.js"
            }
        }
    }
}
