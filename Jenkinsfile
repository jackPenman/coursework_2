pipeline {
  agent any

    stages {
        stage('Build') {
		  agent {
    docker {
        image 'node:latest'

    }
}
            steps {
                node server.js
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
    }
}


