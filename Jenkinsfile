pipeline{
	tools {
		maven 'mymaven'
	}
	agent any
	stages {
	  stage('checkout the code from git repo') {
		steps {
			echo 'cloning the git repo step'
			git  'https://github.com/Sonal0409/DevOpsClassCodes.git'
		}
	  }

	  stage('compile the code') {
		steps {
			echo 'mvn compile step'
			sh 'mvn clean install'
		}
	  }

	  stage('code review') {
		steps {
			echo 'code review step'
			sh 'mvn pmd:pmd'
		}
	  }

	  stage('unit testing') {
		steps {
			echo 'unit testing step'
			sh 'mvn test'
		}
	  }

	  stage('packaging') {
		steps {
		  echo 'packaging step'
		  sh 'mvn package'
		}
	  }
	stage('Deploying'){
		steps{
			sshagent(['AgentID2']) {
				sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Assignment3_pipeline/target/addressbook.war ec2-user@172.31.10.91:/opt/tomcat9/webapps"
			}
		}
	  }

}
}
