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
                    // Check if WORKDIR exists
                    if (fileExists(WORKDIR)) {
                        echo "Directory ${WORKDIR} already exists."
                        dir(WORKDIR) {
                            // Check if it's a valid git repository
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
                        echo "Creating directory ${WORKDIR} and cloning repository ${GIT_REPO}."
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
