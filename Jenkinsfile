pipeline {
    agent any
    
    tools {
        jdk 'jdk8'
        maven 'maven'
    }

    environment {
        PROJECT_SCM_URL = "git@github.com:lonelymoon57/sample.git"
        PROJECT_SCM_CREDENTIALS = "github-sample"
    }
    
    stages {
        stage('Checkout') {
            steps {
                git url: $PROJECT_SCM_URL,
                    credentialsId: $PROJECT_SCM_CREDENTIALS
            }
        }
        
        stage('Build') {
            steps {
                sh "mvn clean verify"
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                sh "mvn sonar:sonar -Dsonar.host.url=http://host.docker.internal:9000"
            }
        }
    }
}