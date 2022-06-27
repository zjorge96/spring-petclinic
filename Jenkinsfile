pipeline {
    agent any
    tools {
        jdk "java8"
        maven "maven3"
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh "apk add curl"
                sh "mvn clean install"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh "mvn test"
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                if (env.BRANCH_NAME == 'master') {
                    sh "curl -u admin:password -X PUT 'http://172.24.0.3:8082/artifactory/jenkins-artifactory/petclinic.war' -T 'target/petclinic.war'"
                } else {
                    sh "echo 'Not master branch. Nothing to deploy.'"
                }
            }
        }
    }
}
