pipeline {
    agent any

    environment {
        registry = "vendett1/jenkins"
        registryCredential = "33f123c8-1917-4072-aac5-7512c3ef965d"
    }

    stages {
        stage('Building Image') {
            steps {
                bat "docker build -t ${registry}:${BUILD_NUMBER} ."
            }
        }

        stage('Publish Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${registryCredential}", passwordVariable: 'DOCKER_PWD', usernameVariable: 'DOCKER_USER')]) {
                        // Switch to default context to be safe on Windows
                        bat "docker context use default"
                        
                        // Use the variables injected by withCredentials
                        // We use --password-stdin to avoid the security warning
                        bat "echo %DOCKER_PWD% | docker login -u %DOCKER_USER% --password-stdin"
                        
                        bat "docker push ${registry}:${BUILD_NUMBER}"
                    }
                }
            }
        }
    }
}