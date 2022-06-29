pipeline {
    agent any

    environment {
        IP='172.24.0.3' // This is the ip associated with artifactory
        ARTIFACTORY_REPO='jenkins-artifactory' // Insert artifactory repo name
        PACKAGE_TYPE='war' // Check the pom file for the packaging type
        JDK_NAME='java8' // Configure JAVA in Gobal Tool Configuration
        MAVEN_NAME='maven3' // Config MAVEN in Gobal Tool Configuration
        POM_VERSION=readMavenPom('pom.xml').version() // Read the version from the pom file (pipeline-utility-steps plugin required)
    }

    tools {
        jdk "${JDK_NAME}"
        maven "${MAVEN_NAME}"
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
                script {
                    if (env.BRANCH_NAME == 'master') {
                        echo 'Deploying..'
                        // The extra \ at the end of this line is required due to escape it since it is a special character in Groovy.
                        sh "find ./target/ -name *.${PACKAGE_TYPE} -type f -exec curl -u admin:password -X PUT http://${IP}:8082/artifactory/${ARTIFACTORY_REPO}/{}-${POM_VERSION} -T {} \\;"
                    } else {
                        echo 'Not master branch. Nothing to deploy.'
                    }
                }
                
            }
        }
    }
}
