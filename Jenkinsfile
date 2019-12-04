pipeline {
    agent any

  environment {
    registry = "jpenma200/coursework2"
    registryCredential = 'dockerhub'
  }

    stages {
	
	stage('Cloning Git') {
  steps {
    git 'https://github.com/jackPenman/coursework_2.git'
  }
}
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


