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
                sh "curl -u admin:password -X PUT 'http://localhost:8082/artifactory/jenkins-artifactory/petclinic.war' -T petclinic.war"
            }
        }
    }
}
