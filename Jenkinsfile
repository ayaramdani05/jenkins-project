pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-21'
            args '--network host'
        }
    }
    stages {
        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh """
                        mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=java-maven \
                          -Dsonar.projectName='java-maven' \
                          -Dsonar.host.url=http://172.18.0.1:9000 \
                          -Dsonar.token=\${SONAR_TOKEN}
                    """
                }
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }
    }
}
