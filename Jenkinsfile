pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/palK2/testData.git', branch: 'master'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t testdata-app .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm testdata-app ls /var/www/html'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker rm -f testdata || true
                docker run -d -p 80:80 --name testdata testdata-app
                '''
            }
        }
    }
}

