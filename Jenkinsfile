pipeline {
    agent any

    stages {

        stage('Release Gate') {
            when {
                expression { new Date().format('dd') == '25' }
            }
            steps {
                echo "Release allowed today"
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f deployment.yaml
                kubectl apply -f service.yaml
                '''
            }
        }
    }
}
