pipeline {
    agent any

    stages {

        stage('Verify Cluster') {
            steps {
                sh 'kubectl get nodes'
            }
        }

        stage('Deploy Green') {
            steps {
                sh 'kubectl apply -f web-green.yaml'
            }
        }

        stage('Wait For Green Ready') {
            steps {
                sh 'kubectl rollout status deployment/green --timeout=120s'
            }
        }

        stage('Verify Green Pod') {
            steps {
                sh 'kubectl get pods -l app=green'
            }
        }

        stage('Switch Traffic To Green') {
            steps {
                sh 'kubectl patch service bluegreen-service -p "{\\"spec\\":{\\"selector\\":{\\"app\\":\\"green\\"}}}"'
            }
        }

        stage('Verify Service') {
            steps {
                sh 'kubectl describe svc bluegreen-service'
            }
        }
    }

    post {
        success {
            echo 'Blue-Green Deployment Successful'
        }

        failure {
            echo 'Deployment Failed - Rolling Back To Blue'
            sh 'kubectl patch service bluegreen-service -p "{\\"spec\\":{\\"selector\\":{\\"app\\":\\"blue\\"}}}"'
        }
    }
}
