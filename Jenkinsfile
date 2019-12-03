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
 stage('Push image') {
		steps {
        withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            push("${env.BUILD_NUMBER}")
            push("latest")
        }
    }
	}
    }
}
