pipeline {
    agent any

    stages {      // whenever you build project 
        stage('Checkout') {    // whuch stage you 
            steps {
                // Checkout the code from the version control system (e.g., Git)
                checkout scm
            }
        }

        stage('Build') {
        
        steps{
        
        	sh 'git checkout Develop'
        }
            steps {
                // Use Maven to build the Java project
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                // Run tests, assuming Maven test phase
                sh 'mvn test'
            }
        }

        stage('Deploy') {
            when {
                // Only deploy for the 'master' branch
                expression { env.BRANCH_NAME == 'master' }
            }
            steps {
                // Example: Deploy to production
                sh 'mvn deploy -P production'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully"
        }

        failure {
            echo "Pipeline failed. Please check the logs for more details."
        }

        always {
            // Clean up or perform actions that need to happen regardless of success or failure
        }
    }
}
