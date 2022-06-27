pipeline {
    agent any

    stages {
        stage('Build') {
            tools {
                java "java8"
            }
            steps {
                echo 'Building..'
                sh "apk add maven"
                sh "mvn clean install"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                // sh "curl -u admin:password -X PUT 'http://localhost:8082/artifactory/jenkins-artifactory/petclinic.war' -T testing.war"
            }
        }
    }
}
