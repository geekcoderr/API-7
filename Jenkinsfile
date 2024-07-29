pipeline{
    agent any

    environment{
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        WORKDIR = '/var/jenkins_home/workspace/WORK_REPO'
    }

    stage('Cloning the Repository'){
        steps{
            script{
                if (fileExists(CLONE_DIR)) {
                        echo "Removing existing directory ${WORKDIR}"
                        sh "rm -rf ${WORKDIR}"
                }
                echo "Cloning repository ${GIT_REPO}"
                sh "git clone -b ${BRANCH} ${GIT_REPO} ${WORKDIR}"
            }
        }
    }
}