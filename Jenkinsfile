pipeline {
	agent any
	tools {
    	maven 'local_maven'
	}
	stages {
    	stage('clean') {
        	steps {
        	sh "mvn clean"  	 
        	}
    	}
	
    	stage('Build') {
        	steps {
        	sh "mvn compile"  	 
        	}
    	}
   	stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
	stage ('Archive Artifacts'){
		steps{
		archiveArtifacts artifacts: 'target/*.war'
		}
	}
	stage ('Deployment'){
		steps{
	        deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://52.4.127.202:8080/')], contextPath: 'BOOKZY', war: 'target/*.war'
		}
	}
	stage ('Notification'){
		steps{
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "build-alerts@example.com"
		   )
	        }
           }
	
    	
}
}
