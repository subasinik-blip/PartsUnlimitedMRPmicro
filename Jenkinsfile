pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code Pulled From GitHub'
            }
        }

        stage('Deploy Green') {
            steps {
                echo 'Green Deployment Created'
            }
        }

        stage('Health Check') {
            steps {
                echo 'Green Deployment Healthy'
            }
        }

        stage('Traffic Switch') {
            steps {
                echo 'Traffic Switched To Green'
            }
        }
    }
}
