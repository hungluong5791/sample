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
                sh "env | sort"
                sh "mvn clean verify"
            }
        }
        
        stage('SonarQube Branch Analysis') {
            when {
                beforeAgent true
                anyOf {
                    branch 'master'
                    branch 'feature/**'
                }
            }

            steps {
                sh "mvn sonar:sonar \
                    -Dsonar.projectKey=lonelymoon57_sample \
                    -Dsonar.organization=lonelymoon57-github \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=9310f120732a6575d2bdd363b0e88cc77001a216 \
                    -Dsonar.branch.name=${GIT_BRANCH}"
            }
        }
        
        stage('SonarQube PR Analysis') {
            when {
                beforeAgent true
                changeRequest()
            }

            steps {
                sh "mvn sonar:sonar \
                    -Dsonar.projectKey=lonelymoon57_sample \
                    -Dsonar.organization=lonelymoon57-github \
                    -Dsonar.host.url=https://sonarcloud.io \
                    -Dsonar.login=9310f120732a6575d2bdd363b0e88cc77001a216 \
                    -Dsonar.pullrequest.branch=${CHANGE_BRANCH} \
                    -Dsonar.pullrequest.key=${CHANGE_ID} \
                    -Dsonar.pullrequest.base=${CHANGE_TARGET}"
            }
        }
    }
}