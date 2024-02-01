pipeline {
	agent any
	tools {
        	maven 'Maven 3.6.3'
        	jdk 'jdk14'
    	}
	
	stages{
		stage('Checkout Code'){
			steps{
				checkout scm
				}
			}
	
	stage('Build'){
		steps{
			//sh "mvn clean install -Dmaven.test.skip=true"
			sh "mvn clean package"
		}
	}
	
	stage('Archive Artifact'){
		steps{
		archiveArtifacts artifacts:'target/*.war'
		}
	}
	
	stage('deployment'){
		steps{
		deploy adapters: [tomcat9(url: 'http://localhost:8081/', 
                              credentialsId: 'tomcatuser')], 
                     war: 'target/*.war',
                     contextPath: 'app'
		}
		
	}
	
	stage('Notification'){
		steps{
		emailext(
			subject: "Job Completed",
			body: "Jenkins pipeline job for maven build job completed",
			to: "devopseng129@gmail.com"
		)
		}
	}
	}
}
