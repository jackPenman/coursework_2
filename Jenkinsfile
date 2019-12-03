pipeline {
    agent any

    stages {
        stage('Build') {
		agent { docker { image 'node:latest' } }
            steps {
                 sh 'docker build . -t server:1'
            }
        }
		
        stage('Sonarqube') {
		agent any
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


