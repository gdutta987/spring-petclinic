pipeline{
	agent { 
		docker {
			image: 'maven:3.5-alpine'
			label: 'linux01'
		}
	}
	stages{
		stage('Checkout'){
			steps{
				git 'https://github.com/shauryakarn/spring-petclinic.git'
			}
		}
		stage('Build'){
			steps{
				sh 'mvn clean package'
				junit '**/target/surefire-reports/TEST-*.xml'
				archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
			}
		}
	}
}