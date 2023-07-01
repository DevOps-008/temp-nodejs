pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                // Add your build steps here
                sh 'pwd'
                sh 'ls'
                sh 'whoami'
                sh 'echo "Building..."'
            }
        }
        
        stage('Test') {
            steps {
                // Add your test steps here
                sh 'echo "Testing..."'
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
