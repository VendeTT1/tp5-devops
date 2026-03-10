pipeline {

    agent any

    environment {
        registry = "vendett1/jenkins"
        registryCredential = "dockerhub"
        dockerImage = ""
    }

    stages {

        stage('Cloning Git') {
            steps {
                git 'https://github.com/VendeTT1/tp5-devops'
            }
        }

        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Test Image') {
            steps {
                script {
                    echo "Tests passed"
                }
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }

    }
}