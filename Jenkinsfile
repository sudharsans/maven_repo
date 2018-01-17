#!groovy

pipeline {
	stage("Build Backend") {
	     steps {
	     	  sh "cd ~/app/server/"
	          sh "./mvnw install"
	     }
	}

	stage("Build Frontend") {
	     steps {
	     	  sh "cd ~/app/client/"
	          sh "npm install && ng build"
	     }
	}

	stage("Docker Build") {
	     steps {
	      	  sh "cd ~/"
	          sh "docker-compose build"
	     }
	}

	stage("Deploy Docker") {
	     steps {
	          sh "docker-compose up -d"
	     }
	}

	stage("Acceptance test") {
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