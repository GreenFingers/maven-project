pipeline {
	agent any
	stages {
		stage('Build'){
			steps {
				def mvn_version = 'localMaven'
				withEnv( ["PATH+MAVEN=${tool mvn_version}/bin"] ) {
			
					sh 'mvn clean package'
				}
			}
			post {
				success {
					echo 'Now archiving...'
					archiveArtifacts artifacts: '**/target/*.war'
				}
			}
		}
	}
}
