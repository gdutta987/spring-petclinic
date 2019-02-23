pipeline{
	agent { label 'linux01' }
	stages{
		stage('Checkout'){
			steps{
				git 'https://github.com/shauryakarn/spring-petclinic.git'
			}
		}
		stage('Build'){
			agent { docker 'maven:3.5-alpine'}
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
				sh 'sshpass -p jenkins scp target/*.jar jenkins@192.168.50.2:/opt/pet/'
				sh "sshpass -p jenkins ssh jenkins@192.168.50.2 'nohup java -jar /opt/pet/spring-petclinic-2.1.0.BUILD-SNAPSHOT.jar'"
			}
		}
	}
}