pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Sonarqube') {
    environment {
        scannerHome = tool 'SonarQubeScanner'
    }
    steps {
        withSonarQubeEnv('sonarqube') {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sonar-js -Dsonar.sources=." 
        }
    }
}
stage('Build and Push Docker Images'){
    steps{
        script {
            docker.withRegistry('https://registry.hub.docker.com', docker-hub-credentials) {
                def customImage = docker.build(server)
                  push("${env.BUILD_NUMBER}")
                customImage.push("latest")
                sh "docker rmi --force \$(docker images -q ${customImage.id} | uniq)"
            }
        }
    }
}
    }
}


