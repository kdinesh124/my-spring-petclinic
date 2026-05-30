pipeline {
    agent any

    tools {
        maven 'Maven'

    }

    triggers {
        pollSCM('H/5 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kdinesh124/my-spring-petclinic.git'
            }
        }

        stage('Build and Sonar Scan') {
            steps {
                withSonarQubeEnv('sonar') {
                    withCredentials([string(credentialsId: 'sonar_id', variable: 'SONAR_TOKEN')]) {

                        sh """
                        mvn clean verify sonar:sonar \
                        -DskipTests \
                        -Dsonar.projectKey=my-spring-petclinic \
                        -Dsonar.organization=kdinesh124 \
                        -Dsonar.host.url=https://sonarcloud.io \
                        -Dsonar.token=${SONAR_TOKEN}
                        """
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 10, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}