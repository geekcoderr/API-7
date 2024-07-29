pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/geekcoderr/API-7.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building Ban Gyi.."'
            }
        }
    }
}
