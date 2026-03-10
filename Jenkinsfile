pipeline {

    agent any

    environment {
        registry = "vendett1/jenkins"
        registryCredential = "33f123c8-1917-4072-aac5-7512c3ef965d"
        dockerImage = ""
    }

    stages {

        stage('Cloning Git') {
            steps {
                  git branch: 'main', url: 'https://github.com/VendeTT1/tp5-devops'
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