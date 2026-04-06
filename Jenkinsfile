pipeline {
    agent any
    
    tools {
        // Must match the "Name" defined in Manage Jenkins > Global Tool Configuration
        maven 'Maven 3.9.0' 
        jdk 'Java 17'
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your Git repository
                checkout scm
            }
        }

        stage('Build & Package') {
            steps {
                // Runs Maven build; '-B' stands for Batch mode (non-interactive)
                sh 'mvn -B clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    // Archives test results even if the build fails
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }
}
