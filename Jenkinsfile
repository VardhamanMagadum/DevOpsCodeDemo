pipeline{
	tools {
		maven 'mymaven'
	}
	agent any
	stages {
	  stage('checkout the code from git repo') {
		steps {
			echo 'cloning the git repo step'
			git  'https://github.com/VardhamanMagadum/DevOpsCodeDemo.git'
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
			echo 'build number is $BUILD_NUMBER'
		    sh 'cp /var/lib/jenkins/workspace/FinalProject/target/addressbook.war .'
		    sh 'docker build -t myimagejenkins:$BUILD_NUMBER .'
	  }

	}
	stage('Push the image to docker hub'){
		steps{
		     sh 'docker tag myimagejenkins vardhamanm/myimagejenkins:$BUILD_NUMBER'
		     sh 'docker login --username vardhamanm --password Hh@15241524'
		     sh 'docker push vardhamanm/myimagejenkins:$BUILD_NUMBER'
		}
	}
	stage('Deploy the application'){
		steps{
		sh 'docker run -d -P myimagejenkins:$BUILD_NUMBER'
		}
	}	
}
}
