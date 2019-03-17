pipeline {
    agent any
    
    tools {
        jdk 'jdk-8'
        maven 'maven-3'
    }

    environment {
        PROJECT_SCM_URL = "git@github.com:lonelymoon57/sample.git"
        PROJECT_SCM_CREDENTIALS = "github-sample"
    }
    
    stages {
        // stage('Checkout') {
        //     steps {
        //         git url: "$PROJECT_SCM_URL",
        //             credentialsId: "$PROJECT_SCM_CREDENTIALS"
        //     }
        // }
        
        stage('Build') {
            steps {
                sh "env"
                sh "mvn clean verify"
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                sh "mvn sonar:sonar \
                    -Dsonar.projectKey=lonelymoon57_sample \
                    -Dsonar.organization=lonelymoon57-github \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=9310f120732a6575d2bdd363b0e88cc77001a216"
            }
        }
    }
}