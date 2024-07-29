pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/geekcoderr/API-7.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Building Ban Gyi.."'
            }
        }
    }
}
