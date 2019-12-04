pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
			  script {
          docker.build registry + ":$BUILD_NUMBER"
        }
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


