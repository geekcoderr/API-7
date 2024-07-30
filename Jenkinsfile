pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        MAIN_DIR = 'git-repo'
    }

    stages {
        stage('Setup Workspace') {
            steps {
                script {
                    
                    if (fileExists(MAIN_DIR)) {
                        echo "Directory ${MAIN_DIR} already exists."
                        dir(MAIN_DIR) {
                            
                            if (fileExists('.git')) {
                                echo "Pulling latest changes from ${GIT_REPO} branch ${BRANCH}."
                                sh "git checkout ${BRANCH}"
                                sh "git pull origin ${BRANCH}"
                            } else {
                                echo "The directory exists but is not a Git repository. Re-cloning."
                                deleteDir() 
                                sh "git clone -b ${BRANCH} ${GIT_REPO} ."
                            }
                        }
                    } else {
                        echo "Creating directory ${MAIN_DIR} and cloning repository ${GIT_REPO}."
                        sh "git clone -b ${BRANCH} ${GIT_REPO} ${MAIN_DIR}"
                    }
                }
            }
        }
    }
}
