pipeline {
	agent any
	tools {
		maven "maven-3.9.9"
		jdk "java-17"
	}
	stages {
		stage('Clone'){
			steps {
			    git url: "https://github.com/bharathdevust/employee-service.git",
			    branch: "master"
			}
		}
		stage('Build'){
		    steps {
			    bat "mvn clean install -DskipTests"
			}
		}
		stage('Test'){
			steps {
			    bat "mvn test"
            }
		}
		stage('Deploy') {
			steps {
			    bat "docker rm -f employee-server"
			    bat "docker rmi -f employee-image"
			    bat "docker build -t employee-image ."
                bat "docker run -p 8090:8090 -d --name employee-server employee-image"
            }
		}
	}
}
