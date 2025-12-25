pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t testdata-app:latest .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm testdata-app:latest ls /var/www/html'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'master'
            }
            steps {
                sh '''
                docker rm -f testdata || true
                docker run -d -p 80:80 --name testdata testdata-app:latest
                '''
            }
        }
    }
}
