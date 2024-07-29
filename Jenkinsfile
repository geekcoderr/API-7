pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        WORKDIR = 'WORK_REPO'
    }
    stages {
        stage('Setup Workspace') {
            steps {
                script {
                    if (fileExists(WORKDIR)) {
                        echo "Directory ${WORKDIR} already exists"
                        dir(WORKDIR) {
                            echo "Pulling latest changes from ${GIT_REPO} branch ${BRANCH}"
                            sh "git pull origin ${BRANCH}"
                        }
                    } else {
                        echo "Creating directory ${WORKDIR} and cloning repository ${GIT_REPO}"
                        sh "mkdir ${WORKDIR}"
                        dir(WORKDIR) {
                            sh "git clone -b ${BRANCH} ${GIT_REPO} ."
                        }
                    }
                }
            }
        }
    }
}
