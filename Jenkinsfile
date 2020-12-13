pipeline {
    environment {
        imageName = "chrisgallivan/automate-all-the-things-docker"
        registryCredential = 'docker_hub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'npm install-test'
                  }
        }
        stage('Build Docker Image') {
            steps {
                script{
                 dockerImage = docker.build imageName
                }
            }
        }
        stage('Deploy to Docker Hub') {
            steps {
                script {
                    docker.withRegistry( '', registryCredential ) {
                        dockerImage.push("$BUILD_NUMBER")
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
        
}
