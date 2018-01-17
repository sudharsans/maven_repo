#!groovy

pipeline {
	agent any
	environment {
        JAVA_HOME    = '/usr/lib/jvm/jre-1.8.0-openjdk-1.8.0.151-5.b12.el7_4.x86_64'
    }
	stages {
	stage("Build Backend") {
	     steps {
	          sh "cd $WORKSPACE/app/server/ && ./mvnw install"
	     }
	}

	stage("Build Frontend") {
	     steps {
	     	  sh "cd $WORKSPACE/app/client/ && npm install && ng build"
	     }
	}

	stage("Docker Build") {
	     steps {
	      	  sh "cd $WORKSPACE && docker-compose build"
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
	}
	
	post {
	     always {
	          sh "docker-compose down"
	     }
	}

}