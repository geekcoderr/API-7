pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        WORKDIR = 'WORK_REPO' // Use relative paths
    }
    
    stages {
        stage('Cloning the Repository') {
            steps {
                script {
                    def workspaceDir = "${env.WORKSPACE}/${WORKDIR}"
                    
                    if (fileExists(workspaceDir)) {
                        echo "Removing existing directory ${workspaceDir}"
                        sh "rm -rf ${workspaceDir}"
                    }
                    
                    echo "Cloning repository ${GIT_REPO} into ${workspaceDir}"
                    sh "git clone -b ${BRANCH} ${GIT_REPO} ${workspaceDir}"

                    dir(workspaceDir) {
                        echo "Setting remote URL in ${workspaceDir}"
                        sh "git config remote.origin.url ${GIT_REPO}"
                    }
                }
            }
        }
    }
}
