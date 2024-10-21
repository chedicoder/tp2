pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "spring:v1"
        USERNAME = "chedi1"
        TOKEN = credentials('DockerHub')
    }
    stages {
        stage('Clone project') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Build Image') {
            steps {
                script {
                    sh 'docker build -t ${DOCKER_IMAGE} .'
                }
            }
        }
        stage('Deploy Image To DockerHub') {
            steps {
                script {
                    sh 'docker tag ${DOCKER_IMAGE} ${USERNAME}/${DOCKER_IMAGE}'
                    sh 'echo ${TOKEN} | docker login -u ${USERNAME} --password-stdin'
                    sh 'docker push ${USERNAME}/${DOCKER_IMAGE}'
                }
            }
        }
    }
}
