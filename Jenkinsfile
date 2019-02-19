pipeline{
	agent {
		docker {
			image 'maven:3.5-alpine'
			label 'linux01'
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
		stage('Deploy'){
			steps{
				input 'Do you approve this build?'
				echo 'Deploying'
				sh 'scp target/*.jar jenkins@192.168.50.2:/opt/pet/'
				sh "ssh jenkins@192.168.50.2 'nohup java -jar /opt/pet/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar'"
			}
		}
	}
}