pipeline {
    agent any
    
    stages {
        stage('Trivy Scan Repo') {
            steps {
                sh 'trivy fs .'
            }
        }
        
        stage('AWS ECR Login') {
            steps {
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 970355526286.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        
        stage('Docker Image Build') {
            steps {
                sh 'docker build -t 970355526286.dkr.ecr.us-east-1.amazonaws.com/nodejs:v1 .'
            }
        }
        
        stage('Docker Image Push') {
            steps {
                sh 'docker push 970355526286.dkr.ecr.us-east-1.amazonaws.com/nodejs:v1'
            }
        }
        
        stage('Trivy Image Scan') {
            steps {
                sh 'trivy image 970355526286.dkr.ecr.us-east-1.amazonaws.com/nodejs:v1 --severity CRITICAL'
                sh '''
                trivy -q image --exit-code 1 --severity CRITICAL 970355526286.dkr.ecr.us-east-1.amazonaws.com/nodejs:v1"
                  if [ $? -ne 0 ]; then
                        echo "Critical vulnerabilities found. Aborting the build."
                        return
                  fi
                  '''
            }
        }
    }
    
    post {
        success {
            // Actions to perform if the pipeline is successful
            sh 'echo "Pipeline succeeded!"'
        }
        
        failure {
            // Actions to perform if the pipeline fails
            sh 'echo "Pipeline failed!"'
        }
    }
}
