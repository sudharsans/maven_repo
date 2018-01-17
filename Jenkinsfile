#!groovy

pipeline {
	stages("Build Backend") {
	     steps {
	     	  sh "cd ~/app/server/"
	          sh "./mvnw install"
	     }
	}

	stages("Build Frontend") {
	     steps {
	     	  sh "cd ~/app/client/"
	          sh "npm install && ng build"
	     }
	}

	stages("Docker Build") {
	     steps {
	      	  sh "cd ~/"
	          sh "docker-compose build"
	     }
	}

	stages("Deploy Docker") {
	     steps {
	          sh "docker-compose up -d"
	     }
	}

	stages("Acceptance test") {
	     steps {
	          sleep 60
	          sh "ng e2e"
	     }
	}
	
	post {
	     always {
	          sh "docker-compose down"
	     }
	}

}