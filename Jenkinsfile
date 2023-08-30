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
	stage('Building the Docker Image'){
		steps{
		    sh “cp var/lib/Jenkins/FinalProject/workspace/target/addressbook.war .”
		    sh "docker build -t myimagejenkins ."
	  }

	}
	stage('Push the image to docker hub'){
		steps{
		     sh 'docker tag myimagejenkins vardhamanm/myimagejenkins:$BUILD_NUMBER'
		     sh 'docker login --username vardhamanm --password Hh@15241524'
		     sh 'docker push vardhamanm/myimagejenkins:$BUILD_NUMBER'
		}
	}
			
}
}
