pipeline {
    agent { docker { image 'node:latest' } }

    stages {
        stage('Build') {
            steps {
                 sh 'npm --version'
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


