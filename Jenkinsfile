pipeline {
	agent any
  tools {
    maven 'localMaven'
  }
  stages {
		stage('Build'){
			steps {
				sh 'mvn clean package'
			}
			post {
				success {
					echo 'Now archiving...'
					archiveArtifacts artifacts: '**/*.war'
				}
			}
		}
		stage('Deploy to staging'){
			steps {
				build job: 'deploy-to-staging'
			}
		}
		stage('Deploy to production'){
			steps{
				timeout(time:5, unit:'DAYS'){
					input message: 'Approve PRODUCTION Deployment?'
				}

				build job: 'deploy-to-Prod'
			}
			post {
				success {
					echo "Code deployed to production."
				}

				failure {
					echo "Deployment failed."
				}
			}
		}
	}
}
