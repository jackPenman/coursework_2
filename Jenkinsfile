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
         dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
            }
        }
		
		stage('Deploy Image') {
  steps{
    script {
      docker.withRegistry( '', registryCredential ) {
        dockerImage.push()
      }
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

	stage('update application'){
		
		steps{
		sh 'ssh azureuser@40.76.45.129 kubectl set image deployments/coursework2 coursework2=jpenma200/coursework2:$BUILD_NUMBER'
		}
}

    }
}


