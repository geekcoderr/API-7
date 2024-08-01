pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/geekcoderr/API-7.git'
        BRANCH = 'main'
        DOCKER_IMAGE_NAME = 'geekcoderr/api-painter'
        DOCKER_IMAGE_TAG = 'latest'
        DOCKER_CREDENTIALS_ID = 'docker-credential-id-geekcoderr'
        USERN = 'geekcoderr'
        APP_NAME = 'api-painter'
        TAG_NAME = 'latest'
    }

    stages {
        stage('Setting Up WORKSPACE') {
            steps {
                script {
                    echo "Cloning or updating repository from ${GIT_REPO} branch ${BRANCH}."
                    if (fileExists('.git')) {
                        sh "git fetch origin ${BRANCH}"
                        sh "git reset --hard origin/${BRANCH}"
                    } else {
                        sh "git clone -b ${BRANCH} ${GIT_REPO} ."
                    }
                }
            }
        }

        stage('Verify Docker Dependency ') {
            steps {
                script {
                    echo 'Verifying Docker installation...'
                    sh 'docker --version'
                    echo 'Dependency Check Passed...'
                }
            }
        }

        stage('Docker Login') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        sh "echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin"
                        echo 'Docker login successful...'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Building Docker image...'
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} &&  ."
                    echo 'Build Successful for Image'
                }
            }
        }

        stage('Tag Docker Image') {
            steps {
                script {
                    echo 'Tagging Docker image...'
                    sh "docker tag ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ${USERN}/${APP_NAME}:${TAG_NAME}"
                    echo "Tagging Success ..."
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    echo 'Pushing Docker image to Docker Hub...'
                    sh "docker push ${USERN}/${APP_NAME}:${TAG_NAME}"
                }
            }
        }

        stage('Indication Stage') {
            steps {
                script {
                    echo 'Image is Pushed to Docker HUB...'
                }
            }
        }
    }
}
