pipeline {
    agent any
    tools {
        maven 'my-maven'
        jdk 'my-jdk'
    }
    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/Anarghjiju/authentication-service.git', branch: 'main'
            }
        }
        stage('Pre_Build'){
            steps {
                bat "docker rm -f auth_container"
                bat "docker rmi -f auth_image"
            }
        }
        stage('Build') {
            steps {
                bat "mvn clean install -DskipTests"
            }
        }
        stage('Test') {
            steps {
                bat "mvn test"
            }
        }
        stage('Deploy') {
            steps {

                bat "docker build -t auth_image ."
                bat "docker run -p 8090:8090 -d --name auth_container auth_image"
            }
        }
    }
}