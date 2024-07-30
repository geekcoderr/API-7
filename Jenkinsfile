pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        WORK_DIR = 'WORK_REPO'
    }

    stages {
        stage('Setup Workspace') {
            steps {
                script {
                    sh "cd .."
                    if (fileExists(WORK_DIR)) {
                        echo "Directory ${WORKDIR} already exists."
                        dir(WORK_DIR) {
                            if (fileExists('.git')) {
                                echo "Pulling latest changes from ${GIT_REPO} branch ${BRANCH}."
                                sh "git checkout ${BRANCH}"
                                sh "git pull origin ${BRANCH}"
                            } else {
                                echo "The directory exists but is not a git repository. Re-cloning."
                                deleteDir()
                                sh "git clone -b ${BRANCH} ${GIT_REPO} ."
                            }
                        }
                    } else {
                        echo "Creating directory ${WORK_DIR} and cloning repository ${GIT_REPO}."
                        sh "mkdir ${WORK_DIR}"
                        sh "cd ${WORK_DIR}"
                        sh "git clone -b ${BRANCH} ${GIT_REPO} ."
                        
                    }
                }
            }
        }
    }
}
