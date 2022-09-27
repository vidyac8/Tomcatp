pipeline {
	agent any
	tools {
    	maven 'local_maven'
	}
	stages {
	stage ('checkout code'){
		steps{
		checkout scm
		}
	}	
    	stage('Build') {
        	steps {
        	sh "mvn clean install -Dmaven.test.skip=true"	 
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
	//stage ('Archive Artifacts'){
	//	steps{
	//	archiveArtifacts artifacts: 'target/*.war'
	//	}
	//}
	stage ('Deployment'){
		steps{
	        deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://54.221.131.236:8080/')], contextPath: 'BOOKZY', war: 'target/*.war'
		}
	}
	stage ('Notification'){
		steps{
		emailext (
		      subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "vidya.c8@gmail.com"
		   )
	        }
           }
	
    	
}
}
