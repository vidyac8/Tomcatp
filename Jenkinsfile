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


        stage ('Deployment'){
	       deploy adapters: [tomcat9(credentialsId: 'TomcatCreds', path: '', url: 'http://3.95.9.73:8080/')], contextPath: 'webapp', war: 'target/*.war'
	}
	
	stage ('Notification'){
		emailext (
		     subject: "Job Completed",
		      body: "Jenkins Pipeline Job for Maven Build got completed !!!",
		      to: "vidya.c8@gmail.com"
		   )
	}

       post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
}

}
}
}

