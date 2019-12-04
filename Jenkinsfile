pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
			echo 'BUILDING'
                 sh 'export DOCKERID=jpenma200'
				 sh 'docker image build --tag $DOCKERID/server:1.0 .'
				 sh 'docker container run \ --detach \ --publish 80:80 \ --name linux_tweet_app \ $DOCKERID/server:1.0'
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


