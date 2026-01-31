pipeline {
    agent any

    stages {

        stage('Clone') {
            steps {
                git ''
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Stop & Remove Old Container') {
            steps {
                sh '''
                docker stop azure || true
                docker rm azure || true
                '''
            }
        }

        stage('Remove Old Image') {
            steps {
                sh '''
                docker rmi guru || true
                '''
            }
        }

        stage('Docker Image Build') {
            steps {
                sh 'docker build -t reddy .'
            }
        }

        stage('Docker Deploy') {
            steps {
                sh 'docker run -d -p 3124:8080 --name webapp reddy'
            }
        }
    }
}
