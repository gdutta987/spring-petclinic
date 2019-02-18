pipeline{
	agent none
	stages{
		stage('Checkout'){
			agent {
				docker {
					image: 'maven:3.5-alpine'
					label: 'linux01'
				}
			}
			steps{
				git 'https://github.com/shauryakarn/spring-petclinic.git'
			}
		}
		stage('Build'){
			agent {
				docker {
					image: 'maven:3.5-alpine'
					label: 'linux01'
				}
			}
			steps{
				sh 'mvn clean package'
				junit '**/target/surefire-reports/TEST-*.xml'
				archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
			}
		}
	}
}